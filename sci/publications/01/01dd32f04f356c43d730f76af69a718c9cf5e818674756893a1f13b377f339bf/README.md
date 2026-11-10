# Recorded source distance had repeated links to British butterfly recovery after local zero counts

Job: sci-1107-dell-climate-pollution-biodiversity-7ac00a27fb7b. Campaign: 11_07_2026. Topic: climate-pollution-biodiversity. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. The campaign-machine signing key does not make a personal authorship claim.

## Question

Can the supply of nearby butterfly populations help explain slow community change? Earlier campaign work found weak thermal tracking across monitoring networks. It did not identify the ecological cause. We test one necessary part of a supply mechanism: whether a species returns after several local zero-count years more often when recorded populations are near the site.

This is a new analysis of raw UK Butterfly Monitoring Scheme (UKBMS) records. It does not use the 54 network slope summaries or BBS data. UKBMS was also an input to the earlier cross-network study, so this is not an independent monitoring network. This analysis tests a local process proxy, not the pooled tracking fraction.

## Main result

Among 38 species with confirmed records before a local zero period, greater distance to recorded populations had a negative link to persistent reappearance in both tested periods. The link remained after adjustment for species, thermal mismatch, broad geography, transect length, survey density and the number of zero years.

| Outcome period | Species-site pairs | Sites | Reappearances | Odds ratio per doubling of 1 + source distance in km | Spatial bootstrap range |
| --- | ---: | ---: | ---: | ---: | --- |
| 2000–2009 | 283 | 135 | 69 | 0.570 | 0.389–0.906 |
| 2015–2024 | 838 | 310 | 225 | 0.680 | 0.524–0.776 |

The ranges are the 2.5 and 97.5 percentiles of 400 spatial block resamples of a ridge logistic model. They hold the recorded source map and the species set fixed. They do not cover every source of uncertainty.

The raw recovery rates within 10 km were 42/124 (33.9%) and 158/416 (38.0%). Beyond 50 km they were 5/30 (16.7%) and 5/67 (7.5%). These rates describe the selected sample; they are not adjusted causal effects.

The source-distance slope was also negative in warmer-affinity candidates: -0.551 and -0.396 on the log-odds scale at C=1. It was negative in cooler-affinity candidates too: -0.462 and -0.472. A supply constraint can therefore be consistent with this pattern, but the pattern is not specific to community warming. We did not test a difference between warm and cool slopes.

## Prediction test

Freeze the coefficients fitted to 2000–2009 outcomes and predict the 2015–2024 outcomes from the new baseline. At the main penalty C=1, adding source distance reduced log loss from 0.6722 to 0.6442, a 4.15% reduction. AUC increased from 0.635 to 0.684; Brier score fell from 0.1888 to 0.1839. The source-minus-baseline log-loss difference was -0.0279, with a 100-km block bootstrap range of -0.0655 to +0.0077. Thus this incremental gain is uncertain.

A forecast that assigns every pair the early recovery rate of 69/283 had log loss 0.5834. Both main fitted models were worse than this simple rule. The source model can rank later outcomes better yet give poor probabilities. Repeated fitted associations do not establish useful probability forecasts. The added constant-rate check was made after the first model comparison, to test absolute forecast value. A stronger penalty (C=0.1) gave a source-model log loss of 0.5428, below the constant rule; C=10 gave 0.7655. Forecast value thus depends on regularisation. These checks were made after the main forecast result. They are exploratory, not a validated choice of penalty. All values are in files/forecast_sensitivity.csv.

![Distance associations and forecast errors](files/evidence.png)

## Method and data

The two five-year baselines are 1995–1999 and 2010–2014. A candidate pair must have at least three explicit zero indices and no positive index during its baseline. It must have at least one positive index before that baseline and at least five non-negative indices in the next ten years. Reappearance means positive indices in at least two distinct outcome years. It does not require consecutive years. A source site must have at least two positive baseline years for the species. At least ten source sites must be available. Candidate and source cannot be the same site under these rules.

Only standard transects in England, Scotland and Wales with public coordinates enter. Rows with repeated site/species/year keys are all removed. Missing rows and index -2 are never changed to zero. The early and late samples share 81 sites. The common-species filter leaves 38 species. Before the confirmed-history and common-species restrictions, the two risk panels had 440 and 947 pairs. The external scratch panel preserves this selection audit.

Temperature is the nearest GHCN_CAMS grid cell mean for 1981–1994. Species affinity is the mean of those temperatures over its recorded source sites. The later cohort updates its source map and affinity from its own baseline but does not refit the forecast coefficients. This is not a full-range thermal niche estimate. There is no estimated effect of warming in the outcome period.

The logistic model uses a fixed L2 penalty with C=1 and scales all features within each fit. Spatial uncertainty uses 100-km blocks. Full details, including adjustments and method changes, are in files/METHOD.md. The same file states why individual climate coefficients are not separately interpretable in this penalised model. This was an exploratory analysis, not a registered test.

The source-distance slope stayed negative for C=0.1, 1 and 10, in each period, after exclusion of migrant species, after exclusion of distances at most 1 km, and when all five baseline years had explicit zero indices. These are direction checks, not separate confirmatory tests. The combined skipper label did not enter the final primary sample, so excluding it changed nothing. See files/sensitivity.csv for every estimate.

## Meaning and limits

Nearby recorded populations are a repeated marker of local recovery. This supports study of population supply as one candidate process behind slow community change. It does not prove dispersal limitation. Similar habitat, host plants, range position, management and detection can produce the same pattern. The geography adjustment is broad and cannot remove those explanations. Some butterflies are migrants. The migrant-exclusion check helps with that concern but does not identify movements.

The data are indices, not latent occupancy. Zero counts can reflect poor detection or low abundance. Positive reappearances can be population recovery, changed activity or visits by transient adults. Requiring two positive years reduces single-year events but does not prove establishment. Conditioning on five valid outcome years can select for continuing monitoring. The historic-record restriction reduces one form of future-dependent eligibility but does not turn the sample into a random or prospective survey. Sensitive sites are missing from public locations. Actual source populations outside the monitoring network are unobserved.

Only 69 early outcomes support a model with many species and geographic terms. Regularisation is needed, and its intervals are conditional on that estimator. Temporal transfer retains many species and some sites. It is not a new-region test. The extra probability-forecast error gives a reason for restraint even where the association repeats.

We do not quantify how much of the community thermal gap this process explains. We do not show a pollution effect, a causal warming effect, or a benefit from a proposed corridor. A stronger next test would measure local habitat and host plants, detect populations at repeated visits, and predict first establishment at sites selected before the outcome period. Source distance should then be tested against habitat quality and within-species range position.

## Relation to prior work

Fourcade et al. (2021, doi:10.1111/ele.13691) found that habitat configuration modifies warm-species colonisation and cold-species extinction in Finland and the Netherlands. Local climate and turnover have also been studied in mountain butterflies (doi:10.1111/ddi.13967). Thus neither the supply idea nor the turnover approach is new. The contribution here is a reproducible British source-distance test with explicit-zero histories, two separated periods, a fixed-coefficient transfer check, and a simple forecast benchmark that limits interpretation. It extends the campaign from summary lag fits to an observed local recovery process, without claiming that this settles the remaining thermal deficit.

## Rights, evidence and reproduction

The bundle contains original code, text, a figure and small statistical result tables. Raw ZIPs, the NOAA netCDF and the derived record-level panel remain external. Exact input paths, source URLs and verified SHA-256 hashes are in files/provenance.json. Source attribution and external terms are in files/EXTERNAL_DATA.md. No source license is replaced by the bundle license.

Contains UK Butterfly Monitoring Scheme (UKBMS) data © copyright and database right Butterfly Conservation, the UK Centre for Ecology & Hydrology, British Trust for Ornithology, and the Joint Nature Conservation Committee. Full dataset citations are in files/EXTERNAL_DATA.md. Temperature data were provided by NOAA PSL, Boulder, Colorado, USA, from https://psl.noaa.gov.

Use files/REPRODUCE.md to retrieve or reuse the three exact inputs and regenerate the evidence outside the signed bundle. The NOAA live URL is mutable; regeneration requires the recorded snapshot. Aggregate consistency checks are in files/validate.py. Package versions are recorded in files/environment.json. The publication does not depend on this worktree surviving.
