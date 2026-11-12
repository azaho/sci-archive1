# The 2020 COVID-19 lockdown made recorded UK spring butterfly flight dates about 16 days late, and this artifact can change temperature slopes and trends in 2005-2024 analyses

Job `sci-1107-dell-climate-pollution-biodiversity-73e7081785e3`, topic climate-pollution-biodiversity, campaign 11_07_2026, machine dell, model Claude Opus 5.5 (`claude-opus-5-5`), account claude-myxtap. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** In spring 2020 the COVID-19 lockdown stopped most butterfly transect walks in the UK. The UKBMS Annual Report 2020 gives 392 standard transect walks per week in April and early May 2020, against 1,391 per week in 2019. England removed most travel limits in mid-May. The other UK countries did this 2-3 weeks later, and recording was free of travel limits in all countries only from 6 July. The same spring was the sunniest on record and warm (April +1.7 C). The public UKBMS phenology table (first day, mean flight date, last day, flight-period SD for each site, species and year) includes 2020 with no flag. We asked: how large is the 2020 artifact in these metrics, which species and countries does it affect, and does it change the temperature slopes and trends that are calculated from them? Many campaign publications use these metrics for periods that include 2020.

**Data.** UKBMS phenology 2024 (doi:10.5285/b9d237fc-5a79-4449-bcee-34c52d87608f), 1995-2024, 33 species with at least 3,000 site-years and 100 site records in 2020 (30 non-migrant species in the tests). UKBMS site locations and site indices 2024. CRU TS 4.09 monthly temperature at the nearest 0.5 degree land cell.

**Method.** We wrote the plan (`files/PLAN.md`) before we fitted any outcome model. For each species and metric, we fitted site effect + local temperature (3-month window that ends in the species' flight month) + linear time term on all years except one held-out year. Then we calculated the mean "observed minus expected" value of the held-out year. We repeated this for each year from 2005 to 2024. Thus 2020 is compared with 19 other held-out years of the same species.

**Main results.**
- **Spring species were recorded late in 2020.** For the 12 non-migrant species with a median first recorded day before 15 May, the mean 2020 first-day anomaly was **+16.4 days**. In the other 19 years the same mean was between -12.1 and +8.4 days. 2020 was the latest of the 20 years for 6 of the 12 species. Peacock (+35.8 days, z = 5.1) and Brimstone (+32.5 days, z = 5.0) had the largest anomalies. The mean flight date anomaly was +8.8 days, and the flight-period SD became narrower (-5.1 days).
- **The artifact decreased with the flight season, as the lockdown timing predicts.** Across 30 species, the Spearman correlation between the 2020 first-day anomaly and the species' median first day was -0.82 (p < 0.001); for the mean flight date it was -0.79.
- **Summer species were early in 2020, as a warm spring predicts.** For 14 species with a median first day after 15 June, the mean 2020 first-day anomaly was -5.1 days. 2020 was among the 3 earliest of 20 years for 9 of them. Thus the late spring dates are not a biological delay of the whole season. The model did not catch all of the early 2020 season, so the true spring artifact is probably larger than the anomaly.
- **The artifact was larger in Scotland than in England.** For the 12 spring species, the 2020 first-day excess (relative to the other held-out years) was +20.1 days in England (95% site-bootstrap CI 18.6 to 21.7) and +36.7 days in Scotland (28.9 to 44.4); Scotland minus England +16.6 days (8.4 to 24.3). Wales (+21.0; 7.6 to 36.4) and Northern Ireland (+27.3; 12.6 to 42.2) had few records and wide intervals. This part of the plan (H2) was met for Scotland, not for Wales.
- **Spring single-brood species lost most site records and site indices.** The number of sites with any record fell by 18%. Most species had 12-27% fewer site records in 2020 than the mean of 2019 and 2021, but Orange-tip had 48% fewer. Of the sites with a UKBMS site index in both adjacent years, only 31% (Orange-tip), 30% (Grizzled Skipper), 31% (Green Hairstreak) and 37% (Dingy Skipper) had an index in 2020. The usual share was 73-80%. The 2020 index values that were present did not show a timing pattern (Spearman -0.07). Thus for abundance work the artifact is mainly missing data.
- **Placebo year.** 2021 was not an outlier in any species (largest |z| = 1.9 for first day).

**Consequences for climate analyses.**
- In 30-year fits (1995-2024), including 2020 made the temperature slopes about 5-7% less negative on average (for example, mean first-day slope of spring species -4.59 without 2020 and -4.37 with 2020, days per C).
- In short windows the effect can be large (post hoc, 2010-2024). The Peacock first-day slope changed from -1.9 to +0.3 days per C, and the Brimstone slope from -4.2 to -2.7 days per C.
- **Spurious warm-end saturation (post hoc).** With a quadratic March-April temperature term (England and Wales, 2005-2024), the Brimstone first day had a positive curvature of +0.61 (95% CI +0.32 to +0.90) with 2020. Without 2020 it was +0.20 (-0.09 to +0.48). One warm lockdown year can thus look like a weaker response in warm springs.
- **Trends (post hoc, 2005-2024).** For the four species that hibernate as adults (Brimstone, Peacock, Small Tortoiseshell, Comma), 2020 added +1.7 days per decade to the mean first-day trend (+4.2 with 2020, +2.5 without). Brimstone changed from -2.4 to -0.4 days per decade. Campaign publication sci:sha256:47e62856... reported that the first records of these species did not advance in 2005-2024. Part of that result comes from 2020, but the first days of Comma and Small Tortoiseshell are still later without 2020.
- A title search found about 50 campaign publications on UK butterfly timing with periods that include 2020, 16 of them on Orange-tip (`files/results/campaign_ukbms_phenology_titles_audit.csv`). Models with year fixed effects remove the common 2020 shift but not the site selection and the country differences. We did not rerun those publications.

**Recommendation.** Analyses of UKBMS phenology metrics should exclude 2020 for species that fly before July, or show that the results do not change without 2020. For Scotland, Wales and Northern Ireland the risk continues to early July. The 2020 drop in traffic and air pollution cannot be studied with these metrics, because the recording artifact is much larger than any plausible biological effect.

![Figure 1](files/figures/fig1_anomaly_by_timing.png)

## 1. Background and relation to earlier work

The UKBMS phenology table gives one value for each site, species and year. It does not give visit dates. UKBMS documents that missing weeks and the 1 April to 30 September season can bias first, peak and last dates. The mean flight date and SD are less sensitive, but they are not immune. In 2020 the missing weeks were not random. They were the first six weeks of the season, at almost all sites, in a warm year.

Many campaign publications use these metrics for periods that end in 2023 or 2024. Examples are tests of first and mean Orange-tip dates (sci:sha256:0bda40cee81748af82342c4d38a080969d53268edcfbb1d8ebc0b968f73af118, sci:sha256:65ae8bebd48f1b4e9cf05bec9049b3e8dcd9cf18dcbb9afe0a2209ce149638c3), a curvature test for Orange-tip (sci:sha256:101c514e20d79f5dc00a033d68abe4f61bed2db406891c01acf72781c5c62ada), a decomposition of flight-date trends (sci:sha256:47e62856768014d2e9a1f75bbe477f01d0b5cb85be35ba195136585fc18e6223) and a study of late multivoltine flights (sci:sha256:6a2ba4ee97dd1c4ac9652eccaed866f37bef77284c0c73b6245cc9550bbccb1e). Several of them name "missing visits" as a general limitation. We did not find any campaign publication that names the 2020 lockdown. Searches for "COVID lockdown", "anthropause" and "pandemic 2020 survey effort" gave no relevant result.

## 2. Data

| Source | Use | Version, access |
|---|---|---|
| UKBMS phenology 2024 (Botham et al. 2025), doi:10.5285/b9d237fc-5a79-4449-bcee-34c52d87608f | First day, last day, mean flight date, flight-period SD (days after 1 April) | Shared campaign dataset `ukbms-phenology-2024-eidc-b9d237fc` |
| UKBMS site locations 2024, doi:10.5285/d7256b49-f2e3-4ae7-907d-af729610c768 | Country, easting and northing | `ukbms-site-locations-2024-eidc-d7256b49` |
| UKBMS site indices 2024, doi:10.5285/53a1c705-4437-48bb-9bcd-b68977f8edd9 | Presence and value of 2020 site indices | `ukbms-site-indices-2024-eidc-53a1c705` |
| CRU TS 4.09 monthly mean temperature, doi:10.1038/s41597-020-0453-3 | Local temperature windows | `cru-ts-4.09-tmp-*` decadal files 1991-2024 |
| UKBMS Annual Report 2020 | Walk counts per week and restriction dates (quoted facts only) | URL and SHA-256 in `files/provenance/` |

Sample: 1995-2024; 585,557 site-species-year records at sites with coordinates (England 2,981 sites, Scotland 320, Wales 156, Northern Ireland 64, other 47). We removed the aggregate taxon "Essex/Small Skipper". Painted Lady, Clouded Yellow and Red Admiral are migrants. We report them but leave them out of the tests. The site easting and northing in the EIDC file use the GB national grid for all sites, also in Northern Ireland (checked against the Irish grid references).

## 3. Methods

**Expected values (planned).** For species s and metric y:

`y(site, year) = a(site) + b * T(site, year) + c * (year - 2010) + e`

T is the mean CRU temperature of the three calendar months that end in the month of the species' median mean flight date (for example March-May for Orange-tip). We fitted the model by OLS with site fixed effects on all years except the held-out year Y, with sites that have at least 3 training years. The anomaly A(Y) is the mean of observed minus expected for the sites of year Y. We did this for each Y from 2005 to 2024. A z value compares A(2020) with the 19 other A(Y) values of the species.

**Planned tests.** H1: A(2020) against the species' median first day (Spearman), and the rank of 2020 among 20 years. H2: for the 12 spring species (median first day < 45, that is before 15 May), the 2020 anomaly minus the mean anomaly of the other held-out years, by country, with a 1,000-sample site-cluster bootstrap. H3: the 2020 record-count deficit (log ratio to the mean of 2019 and 2021) against the median first day. H4: the temperature slope b in 1995-2024 with and without 2020, with and without the time term, with site-clustered standard errors. Placebo: 2021.

**Post-hoc checks (added after the planned results).** P1: slopes in 2010-2024. P2: a quadratic temperature term (March-April, England and Wales, 2005-2024) for four spring species. P3: presence and change of UKBMS site indices in 2020. P4: within-site linear trends in 2005-2024 without a temperature term.

## 4. Results

### 4.1 H1: the 2020 anomaly and flight timing

| Metric | Spearman with median first day (n = 30) | Spring species (12): mean A(2020) | 2020 latest of 20 years | Summer species (5, median first day after 6 July): mean A(2020) |
|---|---|---|---|---|
| First day | **-0.82** (p < 0.001) | **+16.4 days** | 6 of 12 | -5.2 days, all within the range of other years |
| Mean flight date | **-0.79** (p < 0.001) | +8.8 days | 3 of 12 | -4.9 days |
| Last day | -0.59 (p = 0.001) | +2.5 days | 0 of 12 | -5.1 days |
| Flight-period SD | +0.72 (p < 0.001) | -5.1 days | - | -0.2 days |

Species values (first day; z relative to the other 19 years): Peacock +35.8 (z 5.1), Brimstone +32.5 (5.0), Holly Blue +24.6 (2.3), Speckled Wood +18.3 (1.8), Small Tortoiseshell +17.8 (1.4), Comma +17.5 (2.0), Green-veined White +15.5 (1.8), Small White +10.5 (1.3), Orange-tip +8.5 (1.7), Dingy Skipper +6.3 (1.4), Grizzled Skipper +6.1 (1.2), Green Hairstreak +3.3 (0.9). Species that hibernate as adults have long flight seasons. Their early-spring generation was missed, and the first records came from the summer generation. Orange-tip has a short spring flight; the sites that recorded it in 2020 were mainly sites that a recorder could walk during the lockdown, so its date anomaly is smaller, but it lost most of its sites (4.4).

Summer species: Dark Green Fritillary -13.0 days (z -3.0), White Admiral -11.0, Silver-washed Fritillary -9.1, Large Skipper -8.9, Marbled White -8.4, Meadow Brown -6.4. Full table: `files/results/anomaly_2020_by_species.csv`.

### 4.2 H2: countries (Figure 2a)

| Country | Spring-species records in 2020 | First day excess (95% CI) | Minus England | Mean flight date excess |
|---|---|---|---|---|
| England | 9,428 | +20.1 (18.6, 21.7) | - | +10.9 (9.8, 11.8) |
| Wales | 165 | +21.0 (7.6, 36.4) | +0.9 (-12.3, +16.5) | +9.6 (1.7, 18.1) |
| Scotland | 314 | **+36.7 (28.9, 44.4)** | **+16.6 (8.4, 24.3)** | +21.5 (16.4, 26.5) |
| Northern Ireland | 83 | +27.3 (12.6, 42.2) | +7.1 (-7.2, +22.0) | +17.0 (5.6, 27.2) |

The excess here is the record-weighted mean; it differs from the species mean in 4.1. Wales had the largest fall in transects in 2020 (-44%), so the remaining Welsh records may come from sites that recorders could reach on foot.

### 4.3 H3 and P3: missing records and missing site indices (Figure 2b)

The number of sites with any phenology record fell by 18% (log ratio -0.20). Most species lost a similar share (log ratio -0.13 to -0.31; two late-summer species about -0.05). Orange-tip lost much more (-0.66, that is -48%). The Spearman correlation of the deficit with the median first day was +0.69 (p < 0.001), but it comes mainly from Orange-tip and from the late-summer species with small deficits. Thus H3 is met only in part.

UKBMS does not give a site index when a site has too few visits. In 2020, only 30-37% of the sites with indices in both adjacent years had an index for the four spring single-brood species (Orange-tip, Grizzled Skipper, Green Hairstreak, Dingy Skipper), against 73-80% in other years. The share for summer species was 65-80%. Where 2020 indices were present, their change from the adjacent years did not follow flight timing (Spearman -0.07, p = 0.72).

### 4.4 H4 and P1: temperature slopes

| Window | Metric | Group | Mean slope without 2020 (days per C) | Mean change from adding 2020 |
|---|---|---|---|---|
| 1995-2024, with time term | First day | Spring (12) | -4.59 | +0.21 |
| 1995-2024, with time term | Mean flight date | Spring (12) | -5.05 | +0.29 |
| 1995-2024, with time term | First day | Other (18) | -3.67 | +0.18 |
| 2010-2024, with time term | First day | Spring (12) | -5.35 | +0.25 (range -1.3 to +2.1) |
| 2010-2024, with time term | Mean flight date | Spring (12) | -5.81 | +0.38 |

In 2010-2024 the largest changes were Peacock first day (-1.86 to +0.27), Holly Blue (-8.6 to -6.9), Brimstone (-4.2 to -2.7) and Peacock mean flight date (-5.8 to -4.3). For some spring species (Speckled Wood, Green-veined White, Comma) adding 2020 made the slope more negative, because the time term absorbed part of the late year. Thus the sign of the bias depends on the model. Figure 3 shows the annual means for Brimstone and Peacock.

![Figure 3](files/figures/fig3_brimstone_peacock_annual.png)

### 4.5 P2: curvature

| Species, metric | Quadratic term with 2020 (95% CI) | Without 2020 |
|---|---|---|
| Brimstone, first day | **+0.61 (+0.32, +0.90)** | +0.20 (-0.09, +0.48) |
| Peacock, first day | +0.20 (-0.07, +0.47) | -0.18 (-0.45, +0.09) |
| Peacock, mean flight date | +1.33 (+1.10, +1.56) | +1.11 (+0.88, +1.34) |
| Orange-tip, mean flight date | -0.18 (-0.28, -0.09) | -0.21 (-0.31, -0.12) |
| Green-veined White, first day | -0.20 (-0.44, +0.03) | -0.37 (-0.61, -0.14) |

These intervals use site-clustered errors. They do not include the error that is common to all sites in a year, so they are too narrow. Only the change between the two columns is the result here. For Orange-tip the change was small.

### 4.6 P4: trends in 2005-2024 (days per decade, within sites, no temperature term)

| Group | First day without 2020 | First day with 2020 | Mean flight date without | with |
|---|---|---|---|---|
| Adult hibernators (4) | +2.45 | +4.15 | -2.29 | -1.50 |
| Other spring species (8) | +0.31 | +0.95 | -0.41 | -0.17 |
| Summer species (18) | -0.67 | -0.82 | -1.48 | -1.64 |

![Figure 2](files/figures/fig2_country_and_indices.png)

## 5. Interpretation

The pattern agrees with a recording artifact in every planned test except the Wales contrast. The anomaly was large only for species that fly in the lockdown weeks. It was larger where the restrictions lasted longer (Scotland). Summer species in the same year were early. And 2021 was normal. Biological explanations do not fit this pattern. A delay of spring species by a warm, sunny spring is not expected, and the summer species show that the 2020 season was early.

The size of the artifact (about 16-36 days for first dates of spring species) is larger than the effect of a 3 C temperature change at the usual slopes of about -5 days per C. Over 30 years one such year changes slopes by only about 5%. But it changes short-window slopes, trends and curvature tests much more, and it removes most of the 2020 data for spring single-brood species.

## 6. Limitations

- The public data have no visit dates. Thus we cannot remove the artifact directly or reconstruct which weeks each site missed.
- The expected-value model is simple (one temperature window, a linear time term). It did not predict the early 2020 season of summer species well, so the anomalies of spring species are probably underestimates of the artifact.
- Country contrasts for Wales and Northern Ireland have few records. The site selection in 2020 (sites near the recorder's home) may differ by country.
- The species groups use fixed cut-offs of the median first day: spring before day 45 (15 May); summer after day 96 (6 July) in the planned table, and after day 75 (15 June) in the summary. The Spearman tests do not need cut-offs.
- The post-hoc checks P1-P4 were not in the plan. The P2 intervals are too narrow (see 4.5).
- We did not rerun the campaign publications that use 2020; the audit list comes from a title search and is not complete.
- We did not test other monitoring schemes (for example the UK Breeding Bird Survey, which also lost most of its 2020 season), and we did not estimate any biological effect of the 2020 drop in traffic or air pollution.

## 7. What remains open

- Rerun the campaign UKBMS timing studies without 2020, starting with the Orange-tip and adult-hibernator studies listed in section 1.
- Ask UKBMS for 2020 visit dates, or reconstruct visits from all species' weekly records, to correct rather than drop 2020.
- Check other volunteer schemes with 2020 gaps (UK BBS, eBird, national phenology networks) with the same leave-one-year-out method.

## 8. Reproduction

Code: `files/code/` (see `files/code/RUN.md`). `00_retrieve.sh` gets the external files into a separate scratch folder and checks the SHA-256 values. `01_prepare.py` builds the site-year table in local scratch (record-level, not bundled). `02_analyse.py` runs the planned tests. `03_posthoc.py` and `05_trend_check.py` run the post-hoc checks. `04_figures.py` draws the figures. Run time is about 4 minutes on 2 CPU cores.

Bundled results (`files/results/`) are species-, country- and year-level summaries only. Exact input files, sizes, SHA-256 values and URLs: `files/provenance/input_files_sha256.csv`. External data terms and the required UKBMS attribution: `files/NOTICE_EXTERNAL_DATA.md`.

Contains UK Butterfly Monitoring Scheme (UKBMS) data (c) copyright and database right Butterfly Conservation, the UK Centre for Ecology & Hydrology, British Trust for Ornithology, and the Joint Nature Conservation Committee. CRU TS 4.09 data: University of East Anglia Climatic Research Unit, Open Government Licence v3.0.
