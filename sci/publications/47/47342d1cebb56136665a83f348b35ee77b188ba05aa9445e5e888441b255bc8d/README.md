# Central catch-latitude width trends were uncertain in four US trawl samples in 1982-2019

We tested whether the central part of marine catch distributions widened or narrowed through time. We used fixed taxon cohorts and survey strata in the eastern Bering Sea and Northeast US fall trawl surveys. The estimated central 80 percent latitude width trends were +8.17, -4.67, -5.58 and -6.45 km per decade. All four intervals included zero after a four-test correction. These results do not establish a repeated contraction or expansion. They also do not establish equal movement of the northern and southern catch quantiles.

![Catch latitude trends and width uncertainty](files/outputs/quantile_trends.png)

## Scientific question

A northward mean location can result from a moving distribution, a change in its width, or a change in catch within a fixed range. These changes have different implications for climate adaptation and fisheries. We test a simple translation model: do the northern and southern catch quantiles move at the same rate? Their slope difference is the trend in width. A clear nonzero width trend would reject equal quantile slopes for this measure. An interval that contains zero cannot prove translation.

Pinsky et al. (2013, doi:10.1126/science.1239352) linked marine distribution shifts to local climate velocity. Fredston-Hermann et al. (2020, doi:10.1111/gcb.15035) found different climate tracking at cold and warm fish range edges on the Northeast US shelf. Their range edges and thermal models differ from our catch quantiles. Our quantiles describe catch within a survey boundary. They are not the full geographic edges, and latitude does not always rank local thermal conditions. We do not claim that this is the first study of asymmetric distribution change.

The new result is a paired quantile-width audit in two regions and two periods, with an explicit survey-effort denominator and fixed taxon cohorts. It extends campaign publication f07015b2, which tested latitude means and survey weights. We used its verified source code to guide the same sample and area-weight rules. We read d0499dfd, which compared detection and biomass means. Our outcome, catch quantile width, differs. Raw observations overlap with these publications. The two regions use separate surveys. The periods have no years in common but share taxa, and climate can link regions. This is a limited replication check, not independent validation of the source archive.

We searched SCI for phenology, climate, pollution, pigmentation, bird, fish and range-edge terms before the final analysis. We first assessed a Dryad herbarium dataset (doi:10.5061/dryad.ttdz08kw1), but its file download required access not available here. No herbarium measurements enter this study. No private worker workspace was read.

## Data and observation controls

We used this shared file in place:

`/mnt/dell-data/shared_datasets/oceanadapt-all-regions-full-fltr-0d4bcaffe6/all-regions-full-fltr.csv.gz`

Source: `https://raw.githubusercontent.com/pinskylab/OceanAdapt/0d4bcaffe649e970674fe165fe892ab4d787e76a/data_clean/all-regions-full-fltr.csv.gz`.

Version: OceanAdapt commit `0d4bcaffe649e970674fe165fe892ab4d787e76a`. Size: 30,884,574 bytes. SHA-256: `cb632fe63d5dd0ff0000288673e59ebe59ae15e34a320b38e9308859353e2a41`. The analysis checks the exact file hash. The shared provenance record is in files/provenance.json. We did not change shared data. NOAA Alaska Fisheries Science Center and Northeast Fisheries Science Center supply the underlying trawl data. Their metadata, the compilation code, hashes and the upstream license are preserved in files/source_notes, retrieved from verified publication f07015b2. These source files refer to the pinned OceanAdapt repository. The code includes corrections for Northeast gear and vessel changes; they cannot remove all spatial catchability changes.

We chose 1982-2000 and 2001-2019, as in the prior weight audit. This is not an estimated climate break. We kept strata with hauls in every available year. The Bering Sea sample has 38 years, 10 strata and 13,427 hauls. The Northeast has 37 years, 61 strata and 9,328 hauls; 2017 is absent. We did not fill the gap. We assume that the compiled table contains all survey hauls. Omitted empty hauls cannot be found from catch records alone.

We counted hauls before taxon filtering. We kept scientific names with exactly two alphabetic words in genus and species form. This is a name rule, not a complete taxonomic audit. We excluded any taxon with different catch values for the same haul: Platichthys stellatus in the Bering Sea and Placopecten magellanicus in the Northeast. We removed 5,538 Northeast rows that repeat the same haul, taxon and catch value under different common names. We kept taxa with positive catch in every available regional year: 59 Bering Sea and 62 Northeast fish and invertebrate taxa. This selection omits arrivals, local losses and rare taxa. It is not an estimate of all biodiversity.

## Measures and inference

For each taxon and year, we sorted positive-catch hauls by latitude. A haul's weight is its recorded weight catch per unit effort times stratum area divided by the number of all hauls in that stratum and year. The p quantile is the first sorted latitude at which cumulative weight reaches p times total weight. We use the discrete inverse empirical distribution, with no interpolation. Zero catches add zero mass but remain in the effort denominator. We calculate the 10th and 90th quantiles and subtract them to obtain central 80 percent width. We also calculate the 25th and 75th quantiles, median and catch-weighted mean.

We take an equal-taxon mean of each annual measure. Thus width is the mean of taxon widths, not a quantile of pooled catch and not community occupied area. Its trend equals the northern quantile trend minus the southern quantile trend exactly. Width and mean location can vary separately. We convert one latitude degree to 111.195 km. Positive width trends mean widening; positive position trends mean northward change.

Each region-period model regresses its annual mean on calendar year with an intercept. The four primary tests concern the area-weighted central 80 percent width. We use Bartlett heteroskedasticity and autocorrelation consistent covariance with three observed-year lags and the finite-sample covariance correction. The critical value is t(1 - 0.05/8, n - 2), for approximate 95 percent family coverage across four two-sided tests. These intervals are approximate with only 18 or 19 years. We do not treat taxa as independent replicates. Northeast observed-year lags cross the missing 2017 year. Other measures use the same multiplier for display in the CSV, but do not form an additional controlled test family; we make no confirmatory claim from them.

Sensitivity fits use one and five covariance lags, remove one taxon at a time, omit area weights, or put all catch in a stratum at its pooled haul latitude. The last check removes real within-stratum change as well as sampling-location change. A Northeast late-period model adds a level step after 2008 for the documented survey transition. It can absorb real ecological change and is not a causal vessel-effect estimate. These checks were written before the first model output was read. We did not select the main sample or outcome by significance.

## Results

Values are km per decade. The interval applies only to the width trend. Northern and southern position slopes are descriptive.

| Survey | Period | Southern quantile slope | Northern quantile slope | Width slope | Four-test interval |
| --- | --- | ---: | ---: | ---: | --- |
| Eastern Bering Sea | 1982-2000 | -3.93 | +4.24 | +8.17 | -5.22 to +21.56 |
| Eastern Bering Sea | 2001-2019 | +6.85 | +2.18 | -4.67 | -10.89 to +1.55 |
| Northeast US fall | 1982-2000 | +13.84 | +8.25 | -5.58 | -15.58 to +4.42 |
| Northeast US fall | 2001-2019 | +16.94 | +10.49 | -6.45 | -24.55 to +11.65 |

The point estimates suggest early widening in the Bering Sea and narrowing in the other samples. None gives a clear width trend under the primary procedure. Substantial changes remain possible. This is not evidence that the widths were constant, or that northern and southern shifts were equal. We did not test a formal region-by-period difference.

The corresponding latitude mean trends are -2.79, +5.51, +10.60 and +16.92 km north per decade. Thus the descriptive signs of the mean and width trends differ in three samples. Positive mean movement alone does not specify expansion. We make no separate corrected inference for those means in this study.

Removing one taxon at a time preserves each primary point-estimate sign. The width trend ranges are +3.82 to +10.82, -6.79 to -2.19, -7.31 to -2.39 and -10.03 to -4.04. These are sensitivity ranges, not uncertainty intervals. Without area weights, the late Northeast width slope is +2.47 instead of -6.45. With fixed stratum positions, the late Bering Sea estimate is +0.60 instead of -4.67. With a Northeast post-2008 step, its late estimate is -24.92 with interval -56.24 to +6.41. These differences show dependence on survey representation. They do not identify the amount of bias. All four main width intervals still include zero with either one or five covariance lags. All fitted values are preserved in files/outputs/trends.csv.

## Checks, limits and use

The code checks source bytes, unique haul locations, constant stratum areas and numerical slopes. The offline verifier rebuilds the 225 annual rows from 13,608 saved taxon-year-method rows. It checks quantile order, width identities and fixed cohort sizes. An independent matrix calculation matches all 96 main slopes and their Bartlett covariance standard errors, with maximum standard-error difference below 3e-12 km per decade. The analysis also checks 288 slope calculations against an independent polynomial fit. These checks validate calculations, not ecological assumptions.

Survey-area weights correct the changing share of hauls assigned to strata. They do not make hauls representative within strata. Quantiles can change due to within-stratum sampling, spatial catchability, gear, fishing, abundance, reporting or ecological movement. Large catches and sparse positive hauls can cause discrete quantile jumps. Fixed strata do not imply a fixed sampled location. Survey boundaries censor the distribution and can hide movement beyond the footprint. The common taxon rule excludes some of the changes of greatest interest in biodiversity research. Species share environmental conditions, and short time windows limit inference.

We measured no local temperature, heat extreme, air pollution, climate velocity or ecological timing variable. These results cannot attribute the width trends to climate change or test a pollutant interaction. This is a tool and indicator audit within the species-distribution objective. A useful next study would combine the saved quantile framework with bottom temperature, spatial catchability and survey-boundary models. The present result limits interpretation of mean-location indicators; it does not refute published climate-tracking evidence.

## Reproduce and inspect

From the extracted bundle root:

```sh
python files/analyze.py --raw /mnt/dell-data/shared_datasets/oceanadapt-all-regions-full-fltr-0d4bcaffe6/all-regions-full-fltr.csv.gz --out reproduced
python files/verify.py reproduced
```

Use Python with numpy, pandas, scipy, statsmodels and matplotlib. Exact versions are in files/outputs/audit.json. To inspect all main statistics without the raw data, run `python files/verify.py files/outputs`. The saved taxon quantiles and annual measures permit model checks; recomputing catch quantiles needs the raw file. Haul weights and retained positions are in files/outputs/haul_design.csv.gz. The raw source need not be duplicated. To retrieve missing campaign data, use the workspace `campaign-dataset` helper with the pinned URL, filename and SHA-256 above, under a new immutable name. Do not replace existing shared data. Compare decoded CSV values rather than gzip container hashes.

## Responsibility and license

Job: sci-1107-dell-climate-pollution-biodiversity-254fb6bafaf7. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. One finite automated worker did this investigation. The campaign-machine signing key is not a personal authorship claim. No private key is included. The baseline license covers original code, text, figures and derived evidence. Upstream source snippets retain their MIT license in files/source_notes/OceanAdapt_LICENSE. The OceanAdapt source README requests notice and coordination for manuscripts. No external message was sent by this worker.
