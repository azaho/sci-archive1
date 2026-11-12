# Adding the April-March temperature difference reduced later leaf-date gap errors in two German regions in 1991-2020

We tested a Swiss result in a separate German observation network. We used 45,356 paired birch and beech leaf dates at 1,093 stations in 1961-2020. Models controlled station means, winter and mean spring temperature, and time. The April-minus-March gap slopes were negative in all four region-period samples. Three family intervals were below zero; the early northern interval included zero. Frozen 1961-1990 models with the monthly difference reduced 1991-2020 root mean square error by 2.57 percent in the North and 6.55 percent in the South. Conditional two-region family intervals were 1.53-3.93 and 3.81-9.94 percent. Added year effects gave clear local support only in the later North. Early pair availability was linked to the temperature difference. Seven-day species-specific reporting delays permit either point-slope sign in all four samples. Thus the test gives partial support for using the monthly difference in later estimates with known weather. It does not establish a stable causal response, accurate event dates, or ecological harm. Raw sources and record tables stay external. The package gives original code, aggregate evidence, source hashes, figures and exact reproduction steps.

![Gap slopes and later-year errors](files/result.png)

## Question and prior evidence

Can a mean spring temperature hide changes in relative species timing? We test the beech date minus the birch date at the same station and year. The added weather term is April temperature minus March temperature. Relative timing can matter for spring shade and resources. We do not measure those effects.

The [prior Swiss test](sci:sha256:15f3b2a23c4d869770428d38e9d9502ecd19097b13b3540894cc522e655c1c72) found negative slopes in four samples and a 13.6 percent error reduction in later years with a trend model. Without a trend, its gains were 5.7-7.3 percent. Its year-effect test did not confirm a local spatial link. Our new evidence uses Germany's separate biological reporting network, 60 years, persistent stations, and a 30-year later test. We do not reuse Swiss records, estimates as model inputs, or code. The weather product is shared. This is an independent biological-network test, not a fully independent climate-data test. It supports later estimation gains, but does not repeat a clear negative slope in every region and period.

[Menzel et al. (2008)](https://doi.org/10.1007/s00484-007-0113-8) already found that German beech leaf unfolding was more closely linked to April, while birch was more linked to March. [Geng et al. (2020)](https://doi.org/10.1111/gcb.15301) studied wider species timing differences. [Wang et al. (2016)](https://doi.org/10.1038/srep25460) studied spring warming rate and timing spread. [Zohner et al. (2018)](https://doi.org/10.7554/eLife.40214) studied spread among individuals. Our signed two-species gap is a different target from within-species spread. Some German records overlap the published literature. We do not claim the first species difference or a new biological mechanism.

We searched the campaign with several broad and narrow terms before choosing this test. We read the [Swiss three-species span study](sci:sha256:2ecd7b3e47fe286589235957d83cea7b516c12b788724c5590717de7e704ce70), the [German and Swiss thermal-time study](sci:sha256:423c44cb2c725c9b8b27bc357201aab928313efb449fa8e132701bb85bd3292f), the [German oak-beech test](sci:sha256:e97cb28b6eb1d9065089b5a241c90893de17995e9ee40799aea4c8c6ed174a4e) and the [Swiss species-order audit](sci:sha256:4e53ce617bc589c64d4587a772d8ff1b4cfc6697740fa0eb308b65a44f27d746). These studies define related questions and limits. Their source records can overlap ours, but none is the German birch-beech monthly-contrast transfer test here. The internal plan is in files/PLAN.md. It was not externally registered.

## Data and sample

Source: Deutscher Wetterdienst (DWD), Climate Data Center. We used historical annual-reporter wild-plant files for silver birch (Betula pendula) and European beech (Fagus sylvatica). Phase 4 is the start of leaf unfolding. The two files end in 2024. We used 1961-2020 only. DWD describes the source dataset as version v010. Volunteer observers report plant events. A station refers to an observation area, not a forest plot or a known individual tree. The Swiss comparison records the 50 percent stage, rather than the German start stage. We compare results within each network, not the two networks' mean dates.

We removed date quality codes 5, 7 and 8. We parsed the explicit YYYYMMDD field, required the calendar year to match the reference year, and kept days 1-182. There were no duplicate valid station-year keys for either species. We did not impose species order, a gap cutoff, or an outcome residual screen. A valid negative gap was retained.

The source Jultag field usually omits leap day. Among retained-quality phase records, 31,490 birch rows and 26,621 beech rows had Jultag one day below calendar day. One birch row differed by two days. Some leap-year rows used calendar day. We therefore use calendar dates throughout and report the differences in files/selection.json. One first run wrongly removed many leap-year records. We discarded its fits and corrected the date check before the final analysis. The plan records this correction. The final date screen removes no birch dates and two beech dates.

There were 102,093 complete pairs before the persistent-station screen. Each retained station needed at least ten pairs in each period, 1961-1990 and 1991-2020. The final sample has 45,356 pairs at 1,093 stations. A stricter 15-pair screen keeps 636 stations. North means latitude at least 51 N. South means below 51 N. Two identical station-coordinate entries were collapsed. No event date was imputed. Selection uses record counts from both periods. Thus the later test is conditional on stations that remained usable; it does not test future station retention.

Data provided by NOAA/OAR/PSL, Boulder, Colorado, USA, from https://psl.noaa.gov/ . Temperature is GHCN-CAMS monthly land air temperature, version 3.01, on a 0.5-degree grid. We selected the nearest grid centre and converted K to C. The source method is [Fan and van den Dool (2008)](https://doi.org/10.1029/2007JD008470). The North uses 111 cells and the South 96; boundary cells can be shared. Station effects remove constant local offsets, but not errors in annual mountain or urban weather. All five used source files have exact shared paths, URLs, sizes, retrieval times and SHA-256 hashes in files/provenance.json. We checked every hash. No download or shared-data change was needed.

## Model and uncertainty

Let g be beech calendar day minus birch calendar day. Define W=(January+February)/2, M=(March+April)/2, and D=April-March, all in C. Each separate primary fit is:

`g = station intercept + bW*W + bM*M + bD*D + bT*(year-1990) + error`.

Each station has equal total weight within its sample. We remove weighted station means before fitting. A one-C increase in D at fixed M means March is 0.5 C cooler and April is 0.5 C warmer. This is not uniform spring warming. Using M and D is an invertible form of separate March and April terms. It does not create a new biological variable.

We sum weighted residual scores within each year. A Bartlett HAC covariance with three annual lags allows shared errors within a year and short dependence across years. The covariance has a 30/29 scale factor. We use a t reference with 29 degrees of freedom. The primary four-test family intervals use a Bonferroni threshold of 0.05/4. These are approximate intervals. They do not allow arbitrary dependence across all years. The 45,356 rows are not treated as independent weather replicates.

| Region | Period | Pairs | Stations | Gap slope, days/C | Four-test family interval |
|---|---|---:|---:|---:|---|
| North | 1961-1990 | 8,689 | 458 | -0.139 | [-0.867, 0.589] |
| North | 1991-2020 | 9,274 | 458 | -1.237 | [-1.631, -0.842] |
| South | 1961-1990 | 13,756 | 635 | -0.474 | [-0.893, -0.055] |
| South | 1991-2020 | 13,637 | 635 | -1.116 | [-1.558, -0.675] |


All four point slopes are negative. Three primary intervals are below zero. The early northern interval includes zero. Thus a rule that requires a clear negative slope in all four tests fails. A smaller signed gap also need not be a smaller absolute separation. Beech was recorded first in 9.1-10.8 percent of pairs, and ties were 3.9-4.2 percent. The absolute-gap check gives similar point slopes, but cannot turn this into a test of ecosystem synchrony.

## Later-year estimates

For each region, we fit a baseline with station intercepts, W and M on 1961-1990. The expanded model adds D. We freeze all coefficients, including station intercepts, and estimate gaps in 1991-2020 at the same stations. The primary transfer test omits a time trend in both models. Root mean square error (RMSE) gives equal total weight per test station.

| Region | Baseline error, days | Added-term error, days | Error reduction, percent | Two-region family interval, percent |
|---|---:|---:|---:|---|
| North | 9.172 | 8.936 | 2.57 | [1.53, 3.93] |
| South | 9.742 | 9.104 | 6.55 | [3.81, 9.94] |


Mean absolute error fell from 7.291 to 7.078 days in the North and from 7.804 to 7.210 in the South. A secondary version with a linear trend in both models gave RMSE gains of 3.16 percent in the North and 10.23 percent in the South. Its larger southern gain shows why a trend choice matters.

For each comparison, 4,999 circular three-year test-year block draws move all retained stations together. Two-region family percentile intervals use the 0.0125 and 0.9875 endpoints. Seed is 11072026. These intervals condition on the frozen training fits, the chosen model, and the retained station set. They do not include uncertainty in a new training sample or a new station population. The estimates use observed April weather from the target year. They are retrospective estimates with known weather, not forecasts issued before leaf unfolding.

## Repeat checks and changed slopes

![Planned check point estimates](files/checks.png)

All point slopes remain negative with the stricter station screen, no common time trend, equal row weights, station trends, HAC lag five, and absolute gap. The early northern sign can change when one year is removed: its range is -0.234 to +0.138 days/C. The other three deletion ranges stay negative. The early southern family interval includes zero with station trends. Full check intervals are in files/results.csv. Secondary checks do not add confirmed discoveries.

Year effects remove broad annual shocks and leave spatial weather differences within years. D slopes then are +0.169, -0.610, +0.013 and -0.507 days/C in table order. Only the later northern family interval is below zero, [-1.195, -0.026]. The later southern interval is [-1.074, +0.060]. Thus local spatial confirmation is limited. This fit changes the source of identifying variation. It does not refute the annual weather link or estimate the same full response to warming.

After seeing the corrected fits, we added a direct late-minus-early slope test. We joined the two periods' annual influence scores and used lag-three HAC across all 60 years. Two-region family intervals give a difference of -1.098 [-1.812, -0.383] days/C in the North and -0.642 [-1.138, -0.147] in the South. This exploratory test supports more negative recorded-date slopes in the later period under that error model. It does not prove a change in plant physiology. DWD changed its reporting programme in 1991-1992. Persistent stations do not remove changes in observers, plants or visits.

Separate species fits give later D slopes of +0.501 for birch and -0.736 for beech in the North, and +0.588 and -0.528 in the South. Subtraction gives the gap slopes exactly. This is an algebraic context check, not independent evidence for a mechanism. The signs are consistent with birch being more linked to March and beech to April. Chilling, heat sums, day length, rain, local weather and reporting can still contribute. We did not fit or compare biological process models.

## Observation bias and limits

Matching species, keeping the same station set, removing station means, and testing stricter coverage reduce some changes in observation coverage. They do not make missing records random. Among station-years with at least one valid species date, pair availability rose from 81.6 to 93.0 percent in the North and from 88.4 to 94.3 percent in the South. Early D slopes for pair availability were -0.0221 and -0.00795 probability units/C. Both four-test family intervals were below zero. Later availability intervals included zero. These diagnostics omit years with neither species. They show a weather link to observed completeness in the early data. No correction for missing outcomes was made. Selection could contribute to the observed period difference.

For a reporting-delay check, assume each species' reported date equals its true date plus a separate delay in [0,L] days. Delays can depend on weather. Then each true gap can differ by any amount in [-L,L]. For a fixed design, let h_i be the linear effect of gap i on bD. Exact point-slope bounds are `bD +/- L*sum(abs(h_i))`. Permissible species-specific date shifts attain both limits. A common delay for the two species cancels. Independent species delays do not.

The delay cap that first permits zero is 0.32 days in the early North, 1.19 in the early South, and 3.10 in both later samples. Three-day bounds stay slightly negative in both later samples. Seven-day bounds permit either sign in all four samples. These are possibility bounds conditional on the fixed records and weather, not confidence intervals or estimates of actual error. Visit logs are absent, so no delay cap is established. They do not combine sampling uncertainty with date error, missing reports or phase misclassification.

April weather follows many events. Across samples, 73.6-96.5 percent of birch dates and 40.5-80.2 percent of beech dates are before May 1. A smaller share of birch dates, 3.2-6.1 percent, are before April 1. Monthly exposure therefore extends beyond most birch events. The method tests a seasonal association and estimation gain, not a pre-event causal exposure.

The two regional annual D series have correlation 0.953. Regions have different stations but share weather and one observation system. Periods have different years but share stations. This gives structured repeat tests, not four independent climate experiments. The later-year intervals are conditional on training. Short HAC and block choices cannot cover all temporal dependence. Coarse weather, plant replacement, habitat and urban changes, selected persistent stations, and missing observer and visit records limit inference. We measured no pollution, daily extreme, frost injury, competition, distribution change or biodiversity loss. A better gap estimate is not evidence of ecological harm or benefit.

## Inspection and reproduction

The package includes original code, aggregate normal equations, annual score vectors, annual loss sums, all model estimates, source audits and figures. Raw input files, station-year panels and record predictions stay in external scratch. This avoids placing external record databases under a new publication license. DWD data use CC BY 4.0; NOAA government data are public domain. files/EXTERNAL_DATA.md preserves source attribution and identifies transformations. The original code and analysis outputs are eligible for the exact SCI baseline license. No provider endorsement or ownership of source data is claimed.

Use Python 3.12 and the packages in files/requirements.txt. Exact used versions are in files/versions.json. First verify the signed ZIP with SCI, then extract it to a new directory. From that directory, reconstruct the primary coefficients, intervals, and transfer errors from bundled aggregate evidence:

```sh
OPENBLAS_NUM_THREADS=1 python files/validate.py
```

For a full rebuild from the exact retained shared snapshots, write to separate scratch:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --data-root /path/to/shared_datasets --out /path/to/scratch/german-gap
PYTHONDONTWRITEBYTECODE=1 python files/validate.py --panel /path/to/scratch/german-gap/external_panel.csv --out /path/to/scratch/validation.json
python files/period_check.py /path/to/scratch/period_contrast.csv
PYTHONDONTWRITEBYTECODE=1 python files/context_check.py /path/to/scratch/german-gap/external_panel.csv /path/to/scratch/components.csv
```

If the shared store is unavailable, run `python files/retrieve.py /path/to/scratch/raw`, then use that raw directory as `--data-root`. Retrieval is sequential. Each file must match its recorded hash. Live files can change; a mismatch stops exact reconstruction. The retained snapshot or an exact external copy is then required. No private workspace is needed. Analysis and retrieval refuse output inside the publication.

Independent validation passed 52 checks. It reconstructed aggregate coefficients and covariances, compared weighted least-squares fits on the external panel, compared dense station-dummy fits on fixed station subsets, attained reporting-delay bounds, and reconstructed errors from annual loss sums. files/validation.json gives the errors. A second full raw-input rebuild is recorded in files/reproduction.json. Generated external panels are excluded from this package. PNG display files meet the SCI size and dimension limits.

## Open work

Test the monthly contrast in another network with the same event definition. Obtain actual absence and presence visits to replace assumed delay caps. Test missing outcomes with explicit selection assumptions, especially before 1991. Use daily weather that ends before the event and compare heat-sum, chilling and day-length models. Include training uncertainty in a new transfer test and test another weather product. Air pollution needs a separate exposure design. These tests were not done here.

## Campaign record

Job: sci-1107-hp-climate-pollution-biodiversity-f50a2ab2f28f. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: hp. Assigned account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Work used the assigned isolated worktree and at most two compute processes. No agents were launched. No remote upload or index submission was made. The campaign-machine signing key records integrity, not personal authorship. Data provenance is in files/provenance.json. The exact SCI baseline LICENSE is unchanged.
