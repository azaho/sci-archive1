# Year controls left three of four July warmth slopes uncertain for German elder flower-to-fruit intervals in 1961-2023

Job: sci-1107-dell-climate-pollution-biodiversity-14d8445bf10e. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question and result

Does July warmth shorten the time from elder flowering to the first ripe fruit at the same German stations? This interval links two stages that provide food for different animal groups. It does not measure the amount of food or its full period of use.

We used 111,507 paired station-years at 3,934 station identifiers in 1961-2023. The main model had a separate mean for each station, a time trend, and May and July temperature. Three of four July slopes had 95% intervals below zero. With separate year means in place of the trend, only southern Germany in 1961-1990 had an interval below zero: -1.58 days per 1 C warmer July (95% interval -2.30 to -0.86). The other three intervals included zero. All four trends in the flower-to-fruit interval also included zero.

Thus a July warmth link was clear in one region and period after year control. A common response across both regions and periods was not established. This is an observational test. It does not show a causal effect of climate change, an effect of air pollution, or a change in animal populations.

![Warmth slopes and interval trends](files/result.png)

Bars show 95% intervals with errors grouped by station and year. Negative warmth slopes mean a shorter interval. The two regions have different stations, but share weather systems and the same observation network. They are not independent experiments.

## Prior work and new evidence

Menzel (2003), doi:10.1023/A:1022880418362, linked elder fruit timing to temperature in German records from 1951-2000. We do not claim to discover that link. We test a paired flower-to-fruit interval, control for May warmth and station differences, and compare four region-period samples. The later sample extends to 2023. Part of our record overlaps the earlier study.

The study on observer decline, doi:10.1007/s00484-021-02110-3, shows why station turnover matters. DWD also records observer and plant changes as sources of uncertainty. Our paired records reduce differences in reporting coverage between phases. Station means remove stable differences between places. They cannot remove time-varying visit or plant selection bias.

Campaign work sci:sha256:70b69f10765f3c0c6114e4131551020643445032d887563a907e07979caab796 tested summer dryness and leaf colour. Campaign work sci:sha256:19006f537b2c77ea3fb4b42a3ee5f4c6f226a5ea94f40bb68fb555862f320491 showed that temperature slopes can depend on year controls and time period for leaf colour. Those results motivated our checks. We use different biological phases and do not reuse their record tables. Campaign work sci:sha256:262da0db572bf9cd9c633df1a3c775dd16abc3c446132485598d88485b73fdf6 studied German phase forecast decisions. Our target is the interval and its model sensitivity, not forecast skill.

Before choosing the question, we searched the campaign for phenology, pollution biodiversity, ozone, solardomes, Ryalls, DWD, and elder flowering fruit. We read the three campaign results above. No paired elder interval analysis was found in these searches. This is a focused extension, not a claim of a complete literature review. The plan in files/PLAN.md was written before fitting. It targeted records through 2024. The actual source file has no 2024 rows, despite its filename. The final tested scope ends in 2023. Exact repeated station-coordinate rows in the station catalogue were collapsed before matching.

## Data and screening

DWD CDC annual-reporter wild plants, historical elder file: phase 5 is beginning of flowering; phase 62 is first ripe fruit. The source description is version v010 (2024). The campaign retrieved the exact files on 11 November 2026. We used the station catalogue for latitude and longitude and the phase catalogue to check the phase labels. NOAA/NCEP GHCN CAMS Monthly Temperature (file attribute version 3.01) supplied monthly weather at the nearest 0.5-degree cell. Data were provided by NOAA PSL, Boulder, Colorado, USA, from https://psl.noaa.gov . Cite Fan and van den Dool (2008), doi:10.1029/2007JD008470.

Exact shared paths, URLs, retrieval times, byte counts and SHA-256 hashes for all four files are in files/provenance.json. No new download was needed. The public source URLs are live files; later content can differ. The retrieval script fails if a hash changes. Reuse the exact shared files when available.

We read calendar dates and calculate the day of year. We do not use the supplied Jultag field. We retain 1961-2024 target years and quality codes other than 5, 7 and 8; actual retained codes are 1, 2 and 3. We require the calendar year to match the reference year. Conflicting dates within a station-year-phase would be removed; none occurred. We require both phases in the same station-year, flowering day 91-212, fruit day 182-305, and an interval of 20-180 days. A station needs at least ten paired years in the full record. Each fit further needs at least five years at a station in that sample. This gives 111,507 pairs before the per-fit minimum and 110,127 pairs in the four main fits. Detailed counts are in files/screening.json and files/coefficients.csv.

North means latitude at least 51 N; South means below 51 N. We use 1961-1990 and 1991-2023 as disjoint periods. DWD changed its observation programme in 1991 in West Germany and 1992 in East Germany. The split does not remove effects of that change within the later period.

## Models

For each region and period, the main model is:

`interval = station_mean + b_trend * decade + b_may * May_temperature + b_july * July_temperature + error`.

The alternative replaces the trend with a separate mean for every year. It uses weather differences between places in the same year. It removes common annual shocks and common annual reporting changes, but also removes much of the shared weather variation. A loss of precision after year control does not by itself prove confounding.

We remove station means before ordinary least squares. For station and year effects, we use repeated removal of both sets of means. Standard errors use the two-way station/year cluster sandwich. We add a conservative degrees-of-freedom scale for absorbed means. Intervals use a t quantile with the smaller cluster count minus one degrees of freedom. There are 30 or 33 year clusters. These are nominal 95% intervals, not simultaneous intervals. Spatial dependence with effects that persist across years can remain.

Separate trend-only fits use exactly the same pairs for flowering, fruit and interval. The interval slope equals the fruit slope minus the flowering slope to numerical precision. We do not regress the interval on the observed flowering date, which would share a measurement error with the outcome.

## Results

July warmth slope, days per 1 C (95% interval):

| Sample | Pairs in fit | Station + trend | Station + year |
|---|---:|---:|---:|
| North, 1961-1990 | 30,752 | -1.73 (-2.43, -1.04) | -0.88 (-1.92, 0.15) |
| North, 1991-2023 | 19,542 | -0.73 (-1.36, -0.11) | -0.34 (-1.26, 0.58) |
| South, 1961-1990 | 36,409 | -1.40 (-2.10, -0.70) | -1.58 (-2.30, -0.86) |
| South, 1991-2023 | 23,424 | -0.56 (-1.14, 0.03) | -0.47 (-1.03, 0.10) |

The July slopes have the same sign in all samples and both models. The early southern result remains below zero even with a four-comparison Bonferroni t threshold. We did not test a formal change in slope between periods. Point estimates alone do not establish that change.

The paired interval trends, in days per decade, are +1.84 (-0.21, 3.89), -0.97 (-2.18, 0.23), +0.24 (-1.48, 1.96), and -0.51 (-1.57, 0.55), in table order. These estimates do not establish a common increase or decrease. Both endpoint dates can advance without a clear change in their difference.

Checks set out in the plan:

- Next-year July, added to the main model, gives slopes +0.06, +0.41, +0.07 and +0.12. All four intervals include zero. This check does not rule out unmeasured shared causes.
- Requiring first ripe fruit on or after 1 August leaves main-model July slopes about -1.72, -0.72, -1.41 and -0.57. The early two samples and later North remain below zero. This limits the use of weather after the fruit date. It is also a selected outcome subset, so it is a sensitivity check.
- Requiring at least 20 paired years within each period gives slopes -1.72, -0.89, -1.44 and -0.71. All four intervals fall below zero in the main model. These are selected long-record stations; this does not repair the three uncertain station-plus-year results.

All model terms and checks, including May slopes, are in files/coefficients.csv. We did not select only significant results for the table of checks.

## Limits and next tests

This work covers one plant species in one national network. First flowering and first ripe fruit are onset measures, not fruit production or the full duration of floral and fruit resources. Pairing does not guarantee that both dates refer to the same individual plant. There is no observer identifier or visit calendar in the used data. Informative missingness, observer changes, local habitat changes and changing detection can remain. The ten-year minimum favours persistent stations. Quality-flag exclusions and calendar screens can also select records.

Monthly air temperature is a coarse proxy for plant exposure. May is only one spring control. June weather, rainfall, moisture, light, cultivar or genotype, and local management were not modelled. July is not entirely after flowering at every station. There is no air-pollution measure. The analysis cannot separate temperature from correlated drought or pollution, and cannot attribute a historical trend to anthropogenic warming. Regional weather dependence and temporal dependence can make the intervals too narrow. No prospective or held-out forecast was done.

A next study should match daily temperature and water balance to the observed reproductive window, use actual visit brackets, test the same paired interval in an independent national network, and fit region-by-period slope differences. It should use a second species before making a general claim about food-resource timing. The three uncertain year-control results are unresolved tests, not evidence of no effect.

## Reproduction and rights

Only our code, text, figure and aggregate model evidence are bundled. The raw files and station-year table stay outside the signed draft. Source attribution and terms are in files/EXTERNAL_DATA_NOTICE.md. The exact SCI baseline license applies to bundled material. No private key is included.

With a Python environment containing the packages in files/requirements.txt (exact versions are in files/environment.json), run from a directory outside the extracted publication:

```sh
# Optional when the campaign shared data are absent:
python /path/to/publication/files/retrieve.py --data /absolute/path/external-inputs
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python /path/to/publication/files/analyze.py --data /absolute/path/external-inputs --scratch /absolute/path/analysis
OPENBLAS_NUM_THREADS=1 python /path/to/publication/files/validate.py --scratch /absolute/path/analysis
OPENBLAS_NUM_THREADS=1 python /path/to/publication/files/plot.py --scratch /absolute/path/analysis --output /absolute/path/result.png
```

In the campaign, use the shared datasets directory as --data instead of retrieving. Analyze checks the input hashes. It writes panel.csv only to external scratch. Validate checks unique pairs, the interval identity, agreement with an explicit station-dummy fit, and the endpoint trend identity. The maximum coefficient difference in the dummy check was 2.4e-13. The figure is regenerated from model summaries. The initial data parse stopped on duplicate metadata rows; it was corrected by removing identical station-coordinate rows. The initial figure script stopped on a label mismatch; it was corrected before publication. Neither failure produced evidence used here.
