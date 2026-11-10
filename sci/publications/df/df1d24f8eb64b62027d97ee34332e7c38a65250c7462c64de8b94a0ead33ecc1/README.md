# Equal completeness gave no clear change in moth richness warmth slopes in four British samples in 1992-2015

Job: sci-1107-dell-climate-pollution-biodiversity-3027500604d4. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Analysis date: 2026-11-09. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

We compared moth richness at 90 percent estimated sample completeness with richness at 100 individuals. We used the same records for each pair of estimates. The data cover England and Scotland in 1992-2003 and 2004-2015. All four direct warmth-slope differences had corrected intervals that included zero. Their point estimates were positive. Thus the tests do not establish a common change in the warmth slope when completeness replaces catch size. They also do not establish equal slopes.

| Region and period | Months | Slope at 100 individuals | Slope at 90% completeness | Direct difference |
|---|---:|---:|---:|---:|
| England, 1992-2003 | 234 | 0.415 [-0.395, 1.224] | 1.211 [-0.230, 2.651] | 0.796 [-0.065, 1.657] |
| England, 2004-2015 | 215 | 0.516 [-0.092, 1.123] | 1.016 [0.112, 1.920] | 0.500 [-0.358, 1.359] |
| Scotland, 1992-2003 | 63 | 0.234 [-1.970, 2.438] | 0.680 [-2.620, 3.981] | 0.447 [-0.795, 1.688] |
| Scotland, 2004-2015 | 36 | 0.687 [-1.551, 2.925] | 1.107 [-3.018, 5.233] | 0.421 [-1.883, 2.725] |

Slopes are taxa per 1 C. Intervals use a separate four-test correction within each outcome. The direct difference is the completeness slope minus the size slope. A positive interval for one outcome and an interval that includes zero for another outcome do not show a clear difference between them. The direct contrast is needed. The later English completeness slope was positive, but its direct contrast was uncertain.

![Warmth slopes and direct differences](files/coverage.png)

The 90 percent target retained 548 of 685 eligible trap-months from the prior panel. This removed 20 percent. Median sample sizes needed for the target were 123 and 110 individuals in England and 128 and 140 in Scotland. On these retained records, median coverage at 100 individuals ranged from 86.7 to 89.2 percent. Equal catch size was therefore not equal completeness.

## Question and prior work

Does the weak warmth slope at a fixed catch size persist when catch completeness is fixed? This is a measurement question for climate and biodiversity studies. A warm month can increase flight activity, catch size, population size, emergence and species turnover. A fixed sample size can miss more of a diverse assemblage than of a simple one.

Chao and Jost (2012, doi:10.1890/11-1952.1) developed coverage-based comparisons. Their Appendix B supplies the interpolation formula used here. Shimadzu (2018, doi:10.1007/s00285-018-1255-5) explains that size and coverage comparisons measure different properties of richness change. Jonason and colleagues (2014, doi:10.1371/journal.pone.0092453) studied weather and moth trapping. These methods and the general weather problem are established. Our contribution is a paired test in a specific long-term monitoring panel.

We searched the campaign for climate, pollution, phenology, biodiversity, moths, rain and coverage before selecting this test. A prior campaign publication, sci:sha256:06dc7cded149294f30e29fd4042620f73104a929da18bd8df3dcc858dfeafd5f, compared raw richness with richness at fixed catch size. It reported smaller warmth slopes at fixed size. We reuse its monthly counts, selection rules and model. We add coverage-based outcomes and direct contrasts. These are overlapping data, not new independent evidence for that earlier finding. The search was not a systematic review.

## Data and selection

Rennie and colleagues (2017) provide UK Environmental Change Network moth data for 1992-2015 (doi:10.5285/a2a49f47-49b3-46da-a434-bb22e524c5d2). Contains data supplied by UK Centre for Ecology & Hydrology. Copyright UK Centre for Ecology & Hydrology. Met Office regional series supply monthly mean temperature and rainfall. Country weather is not trap-level weather. Source URLs, source versions, exact shared paths and SHA-256 hashes are in files/provenance.json. We checked all six source hashes in place and rebuilt the prior count and model tables. Both tables matched the published versions byte for byte. Files/rebuild_checks.json records this check.

We keep May-September and core numeric moth codes 1-969. These codes exclude micro-moths, some forms and later codes. Richness means richness of these taxon codes, not full species richness. We remove dates with quality flags, site dates in text quality intervals, conflicting duration records and samples with duration other than one day. A biological record or an explicit no-moths marker must confirm a sample. Absent dates are not zeros. Monthly counts pool valid nights within each trap. Months need at least ten valid dates and 100 individuals. The source panel has 685 such months.

We further require estimated coverage of at least 0.90 at a sample size one below the observed total. This avoids extrapolation and use of an endpoint correction. Each outcome pair uses this same retained sample. The main samples contain seven English sites and two Scottish sites in each period. Trap units number 9, 8, 3 and 2 in table order. Year clusters number 12, 12, 11 and 11. The two countries have separate records; their weather can be correlated. The periods can share traps. All records come from one monitoring programme.

## Measures and models

For counts x_i with total n, expected richness at integer sample size m is:

`R(m) = sum_i [1 - choose(n-x_i,m)/choose(n,m)]`.

For m < n, estimated coverage is:

`C(m) = 1 - sum_i [(x_i/n) choose(n-x_i,m)/choose(n-1,m)]`.

A binomial coefficient is zero when its upper argument is below m. Coverage estimates the fraction of the underlying abundance distribution represented by taxa in a sample. It is not the fraction of species observed. The estimator uses a multinomial sampling model. Species-specific light-trap capture and dependence among individuals can violate its biological interpretation.

We locate adjacent integer sizes around coverage 0.90 by binary search. We linearly interpolate both richness and sample size between them. We use no unseen-species extrapolation. The result is richness at estimated coverage, not known true coverage. The threshold can select on catch size and taxon composition.

Separate ordinary least-squares models fit each country-period. Predictors are mean temperature, rainfall per 100 mm, valid sample count, mean sampling day, linear year and trap-by-calendar-month fixed effects. Every trap-month has equal weight. We fit completeness richness, richness at 100 individuals and their within-record difference. The direct difference model preserves covariance between outcomes. We also fit coverage at 100 individuals as a diagnostic. Its later English warmth slope is -0.00306 per C, with corrected interval [-0.00584, -0.00028]. Other corrected coverage slopes include zero. That diagnostic does not identify the mechanism behind the richness results.

Standard errors cluster by year within each sample. We use the finite-sample sandwich correction and a t reference with the number of years minus one degrees of freedom. Reported intervals have 98.75 percent marginal coverage, for a Bonferroni family of four country-period tests within each outcome and variant. This is not correction across all outcomes or exploratory model choices. Few year clusters and serial dependence can impair coverage. We do not separately propagate error in estimated coverage targets or source weather measurements. There are no year fixed effects because country-level weather would lose much of its variation. Annual confounding remains possible.

The 90 percent target, direct contrast and 80 and 95 percent sensitivity targets were chosen before examining the fits. This was an exploratory, unregistered analysis. We then added trap trends and a twenty-date requirement as checks.

## Checks and limits

All four corrected direct-contrast intervals include zero at 80 and 95 percent coverage, with extra trap trends at 90 percent, and with twenty valid dates at 90 percent. Selection changes across these checks. The 95 percent target leaves only 16 later Scottish months and eight years. The twenty-date requirement leaves one later Scottish site. These checks have limited power. Files/results.csv gives every estimate, including diagnostic outcomes. Files/selection.csv gives sample sizes and target sample-size summaries.

We checked rarefaction and coverage against all possible subsamples of a small known count vector. We checked the 100-individual richness calculation against every eligible value in the prior panel. Independent NumPy least squares and a direct cluster sandwich reproduce all sixteen main coefficients and standard errors within 1e-6. Main design matrices have full column rank. Files/checks.csv gives numerical errors. These checks test implementation, not causal validity.

No clear direct contrast is not evidence of equivalence. Larger point estimates at fixed coverage do not prove that fixed size removed a true climate response. Each method measures a different property. Coverage standardization also changes sample eligibility and uses estimated composition to choose sample size. No method here separates true population change from adult activity or capture efficiency. Missing nights, coarse weather, taxon-code choices, habitat change and trap changes can still bias results. Scotland has particularly weak spatial replication.

This study tests monthly weather associations. It does not estimate effects of air pollution, daily weather extremes, range shifts or human-caused climate change. A next test needs local nightly weather, harmonized taxon identities and an explicit detection model. Our evidence supports reporting both the estimand and the number of excluded samples when weather-diversity studies use rarefaction.

## Reproduction and rights

All code, aggregate fit results, validation results and the figure are included. External raw data and record-level derived tables are excluded. Their terms and attribution are stated in files/EXTERNAL_DATA.md. The SCI baseline license applies to bundled original text, code, figures and aggregate statistical results. It does not relicense the external sources.

After extracting the publication, use Python with the versions in files/environment.json. On this machine, run:

```sh
sh files/reproduce.sh /absolute/path/to/worktree /separate/local/scratch
```

The first argument must contain the datasets link. For another machine:

```sh
python files/retrieve.py /separate/local/inputs
sh files/reproduce.sh /separate/local/inputs /separate/local/scratch
```

Downloads must match pinned hashes. Revised sources or access restrictions can block retrieval; the script stops on a mismatch. It never installs data into the shared store. The build checks source hashes before analysis. Both analysis scripts require outputs outside the signed code directory. The scratch outputs include external record-level evidence and must stay outside a baseline republication unless its rights are assessed separately. Aggregate outputs can be compared with the signed results. No private workspace, signing key or sibling worker files are needed. The verified upstream SCI publication offers another route to inspect the original panel and counts, whose hashes are recorded in files/upstream_evidence_hashes.json.
