# Pooling three visits gave no clear relative warmth slope change for two frogs in four US samples in 2001-2015

We tested whether combining three seasonal visits changes the spring warmth slope of recorded frog presence. We compared two indices on the same visits. One index records any call during the year. The other gives the mean detection per visit. We scaled each slope by its index mean.

All eight paired slope differences had intervals that include zero. The estimates range from -2.81 to +0.51 percentage points of relative response per C. The tests cover wood frog and green frog in two US regions and two periods. Planned checks gave the same broad result. Thus, these records do not show a clear common change in relative warmth slopes from this pooling rule. They do not show that either index measures true occupancy without bias.

![Paired index slopes and their differences](files/results/pooling.png)

## Why this question matters

Climate can change when frogs call and when people survey them. A species can remain at a stop but be silent during a visit. A common annual index records a species if any seasonal visit finds it. This rule could reduce missed records. It need not remove the link between weather and recorded presence.

Weir et al. found that season and visit conditions affect anuran detection in Maryland (doi:10.1670/0022-1511(2005)039[0627:MADASO]2.0.CO;2). That work supports models that separate presence from detection. Our comparison concerns two simple recorded-presence indices, not such a model.

Campaign studies found earlier calling after warm springs and changes in survey dates:

- sci:sha256:00fa5e9404f5c28c027c79ca3bc0e3ede118a63b563838d41de45d8e4ad459b1 supplies the verified weather panel and its source builder. It also tested mean run detection, rather than this annual stop index.
- sci:sha256:e90ad89a4e62e9d0968e4b19e07bdba52d25749be30c3eea01a096c9d4ce78e3 shows that the temperature window affects seasonal estimates. We use a fixed March-May window and check February-April.
- sci:sha256:5e672096b5154c6ccca0e28efe751e63a856880c7210b5ba321f3961871a6297 tests whether late visits remain in the public record. We require the same three visits for both indices.

The new evidence is a paired index comparison at fixed stops, observers and visit counts. The package also supplies a checked annual detection-history table. These records overlap the prior studies. Regional and time samples are separate tests within one programme, not independent data sources. Air pollution and daily weather extremes were not tested.

## Data and sample

We use the USGS NAAMP data release for 1994-2015 (Foreman, Grant and Weir, 2017; doi:10.5066/F7G44NG0). The USGS marks this release CC0. The analysis uses unified-protocol records in 2001-2015. Data collection ended in 2015. We acknowledge the NAAMP state partners and volunteers.

Temperature comes from NOAA GHCN-CAMS monthly land air temperature, version 3.01 (doi:10.1029/2007JD008470). Data were provided by NOAA PSL, Boulder, Colorado, USA. March-May and February-April anomalies use 1991-2020 monthly means. Route locations use the median valid stop coordinates. The inherited method uses the nearest 0.5-degree cell, or a local cell mean if the nearest cell is missing.

All raw files already existed in the shared store. We made no downloads. Exact source URLs, shared paths, versions, byte counts and SHA-256 hashes are in `files/provenance/verified_inputs.json`. The weather file hash is `8dbe8e8ce86729f56a2234dec7420b94aecba804aa7df599c8fea68ade70802b`. We rebuilt the inherited weather panel from the raw files. The annual weather CSV matched byte for byte.

Regions are Northeast (NE: ME, NH, VT, MA, NY, PA, NJ) and Midwest (MW: MN, IA, MO, IN, MI). Early means 2001-2008. Late means 2009-2015. The two species are wood frog, *Lithobates sylvaticus*, and green frog, *Lithobates clamitans*.

We kept route-years with exactly one run in each of windows 1, 2 and 3. The same observer had to conduct all three runs. Dates had to follow window order. A stop had to retain its SiteID and StopNumber in all three runs. Each stop had to be explicitly marked as surveyed. We excluded optional visits outside these windows and ambiguous repeated runs. We did not require all ten stops in the main sample.

This build gave 30,889 common stop-years in 3,137 route-years at 618 routes. For each species, we kept routes with at least one detection in the full eligible 2001-2015 record. Each stop-observer group then needed at least two complete years within the fitted period. The eight models use 39,397 species-stop-year records. Species overlap gives 23,188 distinct stop-years at 425 routes. These record counts are not counts of independent temperature observations.

We retained groups with no detections. They form 32-55 percent of fitted stop-observer groups. Route selection by any detection does not establish that every stop is occupied. It can also cause selection bias. Complete schedules need not represent incomplete schedules or routes with no public record.

## Indices, model and uncertainty

Let K be the number of visits with a call, from zero to three. Define U as one if K is positive, and zero otherwise. Define M = K/3. U is annual recorded presence. M is mean detection per visit. Both use identical stops and visits.

For each species, region and period, we fit a linear model:

    index = stop-observer effect + b * spring anomaly + linear year + error

The primary contrast is:

    Delta = 100 * (b_U / mean(U) - b_M / mean(M))

Each component is a percent of its own index mean per C. Delta is their difference, in percentage points per C. It measures a signed change in slope. A negative Delta does not always mean a smaller absolute warmth response. Neither slope is an occupancy effect.

Stop-observer effects remove fixed local and observer differences. The time term removes a linear trend. It does not remove all common annual conditions. The main slope uses annual regional variation as well as local variation. A planned year-effect check instead uses local temperature departures within years.

We use a joint delta method for Delta. It includes uncertainty in both fitted slopes and both sample means. Errors are clustered by route and year, with the route-year intersection subtracted. A common finite-sample factor includes the absorbed effects. The reference t distribution has six or seven degrees of freedom. We report 95 percent limits and 99.375 percent limits for a Bonferroni family of eight tests. The latter have nominal joint coverage of 95 percent only if the separate interval approximations are sound. Few year clusters, spatial dependence and the delta approximation can make actual coverage differ.

The plan was saved before regression fits. After the first history build, we saw that calls were concentrated in one window. We then changed the primary test from raw slope differences to relative slope differences. This change was made before any slope or interval was computed. Raw differences remain in the full results table. `files/code/PLAN.md` records both stages. This is a within-session plan, not an external registration.

## Results

All rates below are descriptive sample rates. Slopes adjust for the stated model effects. Delta limits account for the paired indices and their estimated means.

| Species | Region | Period | Stop-years | Routes | Annual U rate | Mean-visit M rate | U relative slope | M relative slope | Delta | 95% limits | Eight-test limits |
|---|---|---|---:|---:|---:|---:|---:|---:|---:|---|---|
| Wood | NE | early | 4,144 | 105 | 49.8% | 16.9% | +2.41 | +1.90 | +0.51 | -0.98 to +2.00 | -1.92 to +2.94 |
| Wood | NE | late | 3,057 | 95 | 36.3% | 12.3% | -2.10 | -2.50 | +0.40 | -0.78 to +1.58 | -1.58 to +2.38 |
| Wood | MW | early | 6,264 | 162 | 44.9% | 15.3% | -0.34 | -0.77 | +0.42 | -0.49 to +1.34 | -1.07 to +1.91 |
| Wood | MW | late | 5,729 | 141 | 48.5% | 16.5% | -3.00 | -2.65 | -0.35 | -1.33 to +0.63 | -2.00 to +1.30 |
| Green | NE | early | 4,273 | 109 | 45.1% | 17.4% | -1.04 | +1.63 | -2.67 | -10.88 to +5.54 | -16.05 to +10.71 |
| Green | NE | late | 3,190 | 99 | 43.7% | 16.9% | +2.30 | +3.16 | -0.86 | -2.52 to +0.80 | -3.66 to +1.93 |
| Green | MW | early | 5,832 | 156 | 28.7% | 11.2% | -2.82 | -0.02 | -2.81 | -6.15 to +0.54 | -8.26 to +2.65 |
| Green | MW | late | 6,908 | 172 | 36.5% | 14.6% | +2.60 | +2.84 | -0.24 | -1.27 to +0.80 | -1.98 to +1.51 |

Relative slopes are percent of the relevant index mean per C. Delta is in percentage points per C. All eight 95 percent intervals include zero, even before the family correction. The wood frog contrasts have mixed signs. All four green frog contrasts are negative. However, annual slopes are not always closer to zero. Early NE green frog changes sign between indices.

All planned sensitivity contrasts also have 95 percent intervals that include zero. The checks add year effects, change the window to February-April, remove 2012, or use route means from exact ten-stop schedules. Year effects widen the limits and change several estimates. They leave residual temperature standard deviations of only 0.22-0.54 C. The full estimates and support measures are in `files/results/estimates.csv`. This result does not establish equal effects or rule out useful changes for other species.

## Why annual pooling can leave a relative slope unchanged

The index relation has a simple exact form. Let R = K-U be the number of repeat detections after the first. Let p = mean(U) and r = mean(R). Assume p is positive. Since mean(M) = (p+r)/3:

    U/p - M/mean(M) = (r*U - p*R) / (p*(p+r))

If every detected stop-year has exactly one positive visit, R is zero. The two normalized indices are then identical in every row. Their relative regression slopes are equal under any common linear design. This equality can hold even when temperature strongly changes which years have any record. Pooling does not recover a species missed on all visits.

In these samples, only 2.0-2.5 percent of positive wood frog stop-years had more than one positive visit. For green frogs, the range was 15.4-19.8 percent. These counts help explain why wood frog relative slopes change little. They do not prove that the index bias is small. The equation and its row-level checks are in `files/code/audit.py`; aggregate history counts are in `files/results/histories.csv`.

## Checks, limits and next work

An independent sparse model with explicit fixed-effect dummy variables reproduced the eight primary slopes and joint errors. The largest Delta or standard-error difference was below 0.00000000001 percentage points per C. Numerical differentiation checked the ratio gradient. The exact index identity held within 0.000000000000001. The joint covariance matrices were positive definite in all fitted variants.

A separate audit checked all 185,334 bundled binary history values against the raw Counts, Stops and Runs files. It also checked stop identity, observer, window and survey status for every visit. No mismatch was found. These checks test computation and record matching. They do not validate reports or ecological assumptions.

This study cannot separate true presence, calling activity, abundance, pond conditions and hearing. Fixed visit counts remove one source of effort variation, but survey dates and night conditions still vary. We leave these paths in the primary index comparison. The analysis is descriptive and does not identify a causal climate effect. It does not measure long-term distribution change.

The regions omit southern states. The periods contain only seven or eight years and share many routes across periods. Temperature is coarse and may follow some early calls within the March-May window. This is not a forecast exposure. The optional visits are excluded. Selection by complete schedules, repeated observers and any full-record route detection can limit transfer. Remaining spatial dependence can affect errors. The data stop in 2015. Pollution, rain, daily heat, cold events and new recordings remain untested.

A next study should fit dynamic occupancy with a moving seasonal detection curve and all available visit windows. It should test whether the corrected occupancy index changes the warmth slope. Early acoustic recordings would help establish missed wood frog seasons. An independent monitoring programme and later years are needed to test transfer. The checked histories, fixed weather version and source recipes in this package support that work.

## Reproduction and job record

`files/REPRODUCE.md` gives offline analysis, independent checks, raw rebuilds and exact retrieval steps. Outputs must go to separate scratch. The package contains code, derived evidence, aggregate results, source hashes and the figure. Raw third-party files remain outside the publication. Rights and attribution are in `files/EXTERNAL_DATA_NOTICE.md`.

Job: sci-1107-hp-climate-pollution-biodiversity-4be3d103e388. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: hp. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort, through the Codex harness in T3 Code. One worker used at most two CPUs. No sub-agents were used. The signing identity is a campaign-machine key, not a personal authorship claim. This worker signs locally and does not upload or submit the publication.
