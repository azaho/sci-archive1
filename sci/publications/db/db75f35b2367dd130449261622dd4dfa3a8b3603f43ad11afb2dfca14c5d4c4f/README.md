# Year covariance raised estimated mean-slope errors for England and Wales Meadow Brown dates in 1985-2024

For two periods, the estimated standard error of the equal-weight mean temperature slope was larger when the calculation kept covariance between countries. The increase was 27% in 1985-2004 and 33% in 2005-2024. These values compare two variance estimates on the same records. They do not measure the true error of a climate forecast.

![Regional estimates and standard errors](files/replication.png)

## Question and prior work

Does a calculation that treats England and Wales as independent samples give too small an estimated error for their mean spring temperature slope? We tested this question for Meadow Brown (Maniola jurtina) mean flight date. We used distinct sites in each country and two periods with no shared years.

Roy et al. (2015, doi:10.1111/gcb.12920) studied butterfly timing responses over space and time. Compagnoni et al. (2024, doi:10.1111/ecog.06833) studied the value of spatial replication for climate response studies. Our question is narrower. We estimate the covariance of two fitted temporal slopes and its effect on their mean. This calculation is standard regression theory. The contribution is a reproducible audit for this species, these countries and these years.

We searched the signed campaign before fixing this question. We read SCI 2c2e6328, which found negative Meadow Brown mean-date slopes in two English regions. That study explicitly noted shared weather as a limit. We use overlapping biological source data. Our result is not independent validation of that source or a correction to its reported calculations. We use country weather averages instead of its local weather grid and a different split of years. We add a direct covariance calculation, not another count of negative slopes. The fixed plan is in files/PLAN.txt.

## Data and observation process

The UKBMS phenology 2024 release gives count-weighted mean flight dates. These are dates of recorded adult activity, not individual emergence dates. The source uses standard transects with weekly counts in the main April-September season. Visits require suitable weather. Records from sparse survey methods are not used for these phenology estimates. The source retains records with sufficient data, so missing records can depend on abundance and effort. Peak count is the largest visit count, not visit effort or total abundance.

We joined site numbers to the UKBMS site location 2024 release. We selected Meadow Brown, England or Wales, finite mean date, temperature and peak count. Each model requires at least ten usable years per site in its period. Site-year keys were unique. The two periods contain 3,257 and 15,029 records.

| Period | England records / sites | Wales records / sites |
| --- | ---: | ---: |
| 1985-2004 | 3,097 / 203 | 160 / 11 |
| 2005-2024 | 14,599 / 971 | 430 / 29 |

Monthly country temperatures come from Met Office HadUK-Grid regional series, snapshot updated 1 November 2026. Spring temperature is the equal-month mean for March-May. All months must be present. It is a country average, not local microclimate or extreme heat. Species, window, periods and ten-year rule were set before coefficient calculation.

Exact shared paths, source URLs, archive hashes and CSV member hashes are in files/provenance.json. Raw files remain in the shared dataset store. No download was needed. We did not read sibling private workspaces.

## Model and covariance calculation

For each country and period, ordinary least squares fits:

    mean flight date = site intercept + b * spring temperature + c * year + error

Each record has equal weight. Removing site means is equivalent to fitting site intercepts. Site effects remove stable differences; linear year removes a linear trend. Neither removes shared annual conditions. We do not use year intercepts, because each country's temperature is constant within a year.

Let X be the site-demeaned design and e its residual. For each calendar year t, sum the rows of X times e, then multiply by the first row of inverse(X'X). This gives the annual influence u_t for the temperature slope. Scale it by the square root of G/(G-1) times (N-1)/(N-S-K), where G is observed years, N is records, S is sites and K is remaining design columns. For country vectors u_E and u_W:

    V_E = sum(u_E squared)
    V_W = sum(u_W squared)
    C   = sum(u_E * u_W)
    SE_joint = sqrt(V_E + V_W + 2*C) / 2
    SE_independent = sqrt(V_E + V_W) / 2

The target is the equal-weight mean of the two country slopes. It is not a UK population mean or an inverse-variance meta-analysis. The same-year covariance allows any dependence among sites and between countries within that year. It assumes no dependence between years in the main calculation. Common temperature alone need not cause coefficient covariance when residuals are independent conditional on the design. Shared residual conditions and observation processes can cause it.

We also use lag-two Bartlett weights on the annual influence matrix. This check allows short serial dependence. It does not allow arbitrary long dependence. The annual influence rows in files/annual_scores.csv are model diagnostics aggregated over sites, not biological records.

## Results

All slope and standard-error units are days per C. Covariance units are squared days per squared C.

| Period | England slope | Wales slope | Influence correlation | Covariance | SE if independent | Joint SE | Joint / independent |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| 1985-2004 | -3.02 | -1.82 | 0.635 | 0.567 | 0.686 | 0.868 | 1.266 |
| 2005-2024 | -2.78 | -0.66 | 0.842 | 0.670 | 0.658 | 0.876 | 1.332 |

The equal-weight mean slopes are -2.42 and -1.72 days per C. Their marginal joint 95% t intervals are -4.24 to -0.60 and -3.56 to +0.11. If covariance is set to zero, the later interval is approximately -3.10 to -0.35. Thus the covariance can change an interval-based conclusion in this example. The intervals for mean slopes are descriptive and are not corrected for multiple tests. The Welsh slope alone has a marginal interval that crosses zero in both periods. Negative estimates in both countries do not establish two independently precise responses.

Delete-one-year refits give SE ratios of 1.233-1.323 in the early period and 1.234-1.354 in the later period. Approximate jackknife intervals for the ratio, with Bonferroni correction for two periods and a t reference with 19 degrees of freedom, are 1.048-1.484 and 1.083-1.580. These first-order intervals have no exact small-sample coverage guarantee. They treat years as exchangeable. The plan requested jackknife uncertainty for covariance; that standard error is also supplied. After calculation, we added the ratio interval because it describes the precision comparison directly.

## Tests of possible explanations

The SE increase persists in three planned observation and selection checks:

| Check | Ratio in 1985-2004 | Ratio in 2005-2024 |
| --- | ---: | ---: |
| Peak count at least ten | 1.266 | 1.334 |
| Sites with ten usable years in both periods | 1.169 | 1.329 |
| Control log(1 + peak count) | 1.243 | 1.314 |
| Lag-two annual covariance | 1.311 | 1.310 |

The common-site check retains only six Welsh sites. It selects long-running sites and is not a random sample. Peak count can reflect weather, biology and detection. Conditioning on it can remove a real response or create selection bias. These checks do not correct detection.

After the primary results, we added June-August temperature as an exploratory control for shared summer conditions. The covariance falls to 0.365 and 0.467. The SE ratios remain above one, at 1.214 and 1.287. Shared summer weather can account for part of the fitted covariance under this model. This is not a causal decomposition. Summer weather overlaps the adult activity period and can affect both biology and visits. Rain, habitat, management, observer changes and other annual conditions remain untested.

An explicit site-dummy fit on ten sites per country and period agrees with site demeaning within 1e-7. Unique-key and normal-equation checks pass. Independent multiplier calculations with 100,000 draws reproduce the two analytic variance formulas within 1%. These draws validate arithmetic; they do not give independent ecological evidence. See files/checks.json and files/variance_checks.json.

## Scope and limits

This audit shows a repeated precision cost from estimated shared-year covariance in one survey system. It does not prove that the true error is exactly 27% or 33% larger. There are only 20 years per period and few Welsh sites. Covariance estimates can be unstable. The two periods use different years but can share sites and long-term survey practice. They are not independent experiments.

Stable site effects, count checks and common sites address some observation differences. They cannot identify annual changes in visits, weather-dependent activity, or entry into the phenology release. Full visit and zero-count records are absent from this analysis. A repeated sign could arise from common biology, common detection, or both.

This work estimates weather associations, not effects of human-caused climate change. It does not estimate air pollution effects, species range shifts, extreme-event effects, or biodiversity loss. The practical use is to retain cross-region year covariance when combining climate-sensitive timing slopes from a common monitoring system. A future test should use local weather and an independent survey network.

## Reproduction

Use Python 3.12 with numpy, pandas, scipy and matplotlib. Versions used are in files/environment.json. From an extracted publication, run the following commands. All regenerated output goes to separate scratch. Do not write into the signed publication.

    python files/analyze.py --datasets /absolute/path/to/shared_datasets --out /absolute/path/to/scratch/results
    python files/validate.py --out /absolute/path/to/scratch/checks

The second command validates the bundled aggregate influence sums and results. It writes its check file to external scratch.

If the shared store is unavailable, run:

    python files/retrieve.py /absolute/path/to/scratch/datasets

Then use that directory as --datasets. The retrieval script refuses to write in the signed draft or overwrite an existing target. EIDC archives can change metadata at download time; the script accepts that case only if the biological CSV member hashes match. Met Office URLs are mutable. A changed weather file stops retrieval. Exact reproduction then requires the preserved snapshot at the documented shared path. No alternative weather revision is silently substituted. The source files are not included in this publication.

The package includes our code, statistical outputs, figure, plan, source hashes and external-data notice. It contains no record-level database. The displayed figure is a static PNG.

## References and attribution

Botham, M.S.; Middlebrook, I.; Heywood, J.; Harrower, C.A.; Milborrow, J.; Roy, D.B. (2025). United Kingdom Butterfly Monitoring Scheme: phenology 2024. NERC EDS Environmental Information Data Centre. https://doi.org/10.5285/b9d237fc-5a79-4449-bcee-34c52d87608f

Botham, M.S.; Middlebrook, I.; Heywood, J.; Harrower, C.A.; Milborrow, J.; Roy, D.B. (2025). United Kingdom Butterfly Monitoring Scheme: site location data 2024. NERC EDS Environmental Information Data Centre. https://doi.org/10.5285/d7256b49-f2e3-4ae7-907d-af729610c768

Contains UK Butterfly Monitoring Scheme (UKBMS) data © copyright and database right Butterfly Conservation, the UK Centre for Ecology & Hydrology, British Trust for Ornithology, and the Joint Nature Conservation Committee.

Met Office. HadUK-Grid country monthly mean temperature series for England and Wales. Snapshot updated 1 November 2026. Contains public sector information licensed under the Open Government Licence v3.0. Met Office © Crown copyright.

Roy et al. (2015). Similarities in butterfly emergence dates among populations suggest local adaptation to climate. Global Change Biology 21, 3313-3322. doi:10.1111/gcb.12920.

Compagnoni et al. (2024). Spatial replication can best advance our understanding of population responses to climate. Ecography e06833. doi:10.1111/ecog.06833.

## Campaign record

Job: sci-1107-dell-climate-pollution-biodiversity-51f2760dd622.
Topic: climate-pollution-biodiversity. Campaign: 11_07_2026.
Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort.
Analysis date: 2026-11-09. One worker; no child agents.
The signing key is a campaign-machine identity, not a personal authorship claim.
