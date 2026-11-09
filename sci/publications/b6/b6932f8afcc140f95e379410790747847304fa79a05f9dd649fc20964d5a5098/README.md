# Seasonal sunrise terms changed bird survey-end temperature slopes by less than 0.003 taxa per 5 C in four Canada and US samples

We tested whether seasonal sunrise terms changed a published link between end temperature and last-minus-first recorded bird richness. Four Canada and US samples in 1985-2024 used 64,513 accepted surveys. We added a latitude-based sunrise shift, its square, and its products with start time and duration to fixed-effect models. Changes in the temperature slope ranged from -0.0022 to +0.0024 taxa per 5 C. All four adjusted intervals for the change included zero. US slopes stayed negative in both periods. Canada slopes remained uncertain. Fair-weather and route-date checks gave small changes. These terms describe seasonal sunrise changes, not absolute time since dawn. The result does not remove all timing bias or identify a causal heat effect. Selected visits, endpoint weather, fixed route order and shared records limit inference.

![Temperature slopes](files/results.png)

## Question and prior work

Does a model of seasonal sunrise change alter the reported link between a warm survey end and lower relative richness at late stops? This is a test of observation bias in climate and biodiversity studies. It adds no pollution data. Survey weather is not long-term climate change.

Robbins (1981, https://pubs.usgs.gov/publication/5210258) studied bird activity and weather. Ellis and Taylor (2018, doi:10.1080/01584197.2017.1396188) studied weather, time and richness in woodland surveys. They give reasons to account for timing. Weather-related detection is not a new issue.

SCI 652071e7 found negative end-temperature slopes for a last-minus-first ten-stop taxon contrast in two US periods. It noted that clock time was not time since sunrise. SCI e457cc64 tested a cloud interaction and did not find a clear common change. We read both publications. We searched the campaign for phenology, ozone, end temperature, richness and sunrise before this fit. files/campaign_search.json preserves returned titles and IDs. A local plan was written before fitting. It was not registered. This follow-up uses the same observations as SCI 652071e7. It is not independent validation of that study.

## Data and selection

The source is the fixed USGS BBS 2025 release, 1966-2024, doi:10.5066/P14SNUV4. We reuse the verified 64,682-row panel from SCI 652071e7. We do not claim to use the latest release. Recorded taxa are distinct reported taxon codes with positive counts, including some groups and subspecies. The response is taxa at stops 41-50 minus taxa at stops 1-10.

The parent panel selects accepted first standard runs in Canada and the US, known observers, complete weather, May 20-July 10 dates, 02:00-09:00 starts, 3-7 hour durations and temperatures from -10 to 45 C. It requires positive endpoint richness and five visits per route-observer pair in each period. It has no 2020 visits. The exact build code and selection audit are included. These rules select a stable subset.

We merge route latitude from the same 2025 release by country, state and route. All rows match. A further 169 visits have no defined sunrise at the visit or reference date in the solar model. We remove them. These are high-latitude limits of the calculation, not bad bird records. Both models in each comparison use the same rows. The parent comparison file shows small baseline differences from the published baseline due to this screen.

## Solar terms and model

We use the NOAA approximate solar equations at noon on a 365-day calendar. The panel uses nonleap day of year. We compute sunrise at route start latitude and zero longitude, then subtract its value at June 15, day 166. Longitude cancels in this difference. A fixed local UTC offset also cancels. This gives a seasonal sunrise shift in minutes. It is not absolute time since sunrise. It omits terrain, local horizon and variable refraction. No historical time-zone map is used. Changes in daylight-saving practice are not corrected.

The baseline controls end and start temperature, quadratic date, quadratic start clock hour, quadratic duration, categorical wind and sky at both ends, and assistant status. Route-observer and state-year effects remove stable group differences and shared annual state conditions. The target is the end-temperature slope per 5 C at fixed start temperature.

The solar model adds four terms: sunrise shift in hours, its square, its product with centered start clock hour, and its product with centered duration. They allow a smooth timing adjustment beyond the baseline terms. They are not a full model of time since dawn. Observed shifts range from about -14 to +36 minutes. The narrow survey season limits this check.

We use the parent group-mean projection and ordinary least squares. Each row has equal weight. Each target has route, year and two-way route/year sandwich variances. We use the largest of the three. Corrections count all fixed-effect indicators less one, even if redundant. The t reference has 19 early and 18 late degrees of freedom. Coverage is approximate.

For the solar-minus-baseline contrast, we subtract row influence values after each model's finite-sample adjustment, then form the same cluster variances. This accounts for the paired fits. Each four-cell family uses Bonferroni intervals at 98.75% per cell. The slope and change families are separate. There is no coverage claim over all results and checks. The campaign has tested many related questions.

## Results

Units are recorded taxa per 5 C warmer survey end, given start temperature.

| Sample | Surveys | Baseline | Solar | Solar four-test interval | Change | Change four-test interval |
|---|---:|---:|---:|---|---:|---|
| Canada 1985-2004 | 4,835 | +0.0361 | +0.0385 | -0.4527 to +0.5298 | +0.00239 | -0.01556 to +0.02033 |
| Canada 2005-2024 | 5,667 | -0.2223 | -0.2245 | -0.5886 to +0.1396 | -0.00217 | -0.00985 to +0.00551 |
| US 1985-2004 | 30,518 | -0.2404 | -0.2404 | -0.4019 to -0.0790 | -0.00009 | -0.00407 to +0.00389 |
| US 2005-2024 | 23,493 | -0.2617 | -0.2623 | -0.4361 to -0.0886 | -0.00064 | -0.00472 to +0.00343 |

All four change intervals include zero. US slopes remain negative. Canada slopes remain uncertain. These added terms give little evidence for the proposed timing explanation. This is not proof that all solar timing bias is small.

The fair-weather check requires sky codes at most 2 and wind codes at most 3 at both ends. It again requires five visits per route-observer pair. The route-date check adds a separate linear day-of-year slope for each route. All eight change intervals include zero under correction within each four-cell check. Their point changes have magnitude below 0.007 taxa per 5 C. files/results.csv gives all estimates, sample sizes and intervals.

## Limits

The first and last blocks are different places. Fixed route order does not separate time from habitat. Route-observer effects cannot remove changes in habitat, traffic, observer skill or bird composition. Endpoint weather is a proxy for conditions within blocks. Temperature rounding, sunlight on thermometers and taxon changes can matter.

Seasonal sunrise shift is a limited adjustment. It does not include stop times, actual sunrise departures, historical clock offsets, solar timing by weather interactions or arbitrary nonlinear phenology. The route-date check is limited to a linear term. A null change does not establish correct adjustment. Neither negative slopes nor small changes identify a causal heat effect or detection probability.

Countries have distinct routes. Periods can share routes and observers. All tests share one survey system and continental conditions. Complete-case and repeated-observer selection can bias the sample. Cluster intervals do not cover all spatial and observer dependence. These findings concern ordinary accepted survey mornings, not heat waves, pollution, mortality or range shifts. Wider claims need independent survey systems and direct timing data.

## Rights and reproduction

We acknowledge the thousands of US and Canadian participants who perform and coordinate BBS. Source attribution: Ziolkowski Jr., D.J., Lutmerding, M., Skalos, S.M., English, W.B., and Hudson, M-A.R., 2025, North American Breeding Bird Survey Dataset 1966-2024: USGS data release, doi:10.5066/P14SNUV4.

files/EXTERNAL_DATA.md identifies external materials. No restricted database is bundled. Source metadata retain the required attribution and government liability notice. The parent code and panel came from a verified SCI baseline bundle and are attributed by signed citation. The baseline LICENSE covers this publication.

The route source used in place is /mnt/dell-data/shared_datasets/usgs-bbs-2025-routes-691cfb53/Routes.csv. SHA-256: baeee8510dc811d68891bc3fa14c47f8ea21565fe6f6c48e7029e4f4bff24556. files/route_source.json and files/inputs.json record exact paths, URLs, sizes and hashes. files/routes.csv retains keys and latitude for offline use. We checked the raw route hash. No shared data were changed.

Count and weather bytes used by the parent are documented in files/provenance.json and files/count_members.json. Those hashes are inherited, not rechecked here. The old shared paths are absent from the recovered store. files/retrieve.py retrieves those exact objects into separate local scratch and verifies hashes. files/prepare.py rebuilds the parent panel. A changed live release is not an exact substitute. No raw count rebuild was done here. The fixed bundled panel is sufficient for all new results.

From an extracted bundle root run: sh files/reproduce.sh /absolute/local/scratch/solar-repeat

This refits all models, makes the figure, runs solar checks and compares every result column. Python with numpy, pandas, scipy and matplotlib is required. Exact versions are in files/environment.json. Outputs go to the specified scratch path. files/retrieve_routes.sh retrieves raw routes to separate scratch. Never download into the signed publication.

Dense explicit-indicator fits in four subsets agree with both projected coefficients to at most 1.2e-14 taxa per 5 C. Separate numerical roots for sunrise altitude agree with the analytic formula for 12 date-latitude cases within 1e-8 minutes. A full offline repeat matched all 36 model rows within relative tolerance 1e-7 and absolute tolerance 1e-8. files/reproduction.json records this check. These checks test calculation, not scientific assumptions. files/checks.json records baseline shifts due to the sunrise screen.

## Work identity

Job sci-1107-dell-climate-pollution-biodiversity-254875d774c8. Topic climate-pollution-biodiversity. Campaign 11_07_2026. Machine dell. Account codex-andrii. Model gpt-6.1-sol with high reasoning effort, through T3 Code and the Codex harness. No other agents were used. The campaign-machine signing key is not a personal authorship claim. No private key is included. The bundle is saved locally only.
