# Five-year butterfly persistence deficits appeared in both time directions in British records from 1990 to 2019

Job: sci-1107-hp-climate-pollution-biodiversity-2cb451a0e26b. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: hp. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, in T3 Code through the Codex harness. The signing key identifies the campaign machine. It does not make a personal authorship claim.

## Question and result

Can poor persistence after arrival help explain slow community warming? Earlier campaign work found that new taxa stayed rare. It proposed a slow establishment phase as one possible cause. We test a necessary step in that interpretation. Do newly recorded butterfly populations have worse outcomes than established populations that start at similar abundance? Does this contrast depend on the direction of time?

We used UK Butterfly Monitoring Scheme (UKBMS) indices through 2024. We did not use BBS counts or the 54 network slope summaries. UKBMS contributed to earlier campaign work, so this is a new process test on a shared source network, not an independent network replication.

New records after five zero years had lower five-year persistence than matched established records. The same deficit appeared when we reversed time. In real time, these reversed entries were positive records before five zero years. Their outcomes were the preceding five years. Thus the main deficit is not specific to arrival. A mathematical example shows that both deficits can occur with constant population means and no establishment phase.

These results limit what the rarity of newcomers can tell us about the thermal-tracking gap. They do not show that establishment costs are absent, or that observation error explains the gap.

![Evidence from matched records and a stationary model](files/evidence.png)

## Main evidence

Persistence is the fraction of the next five years with a positive index. A deficit is entry persistence minus the mean persistence of its matched controls. Values below are percentage points. Each range is a 95% conditional bootstrap range from 2,000 resamples of 100-km blocks of entry sites.

| Origin period | Forward entries | Forward deficit | Reversed entries | Reversed deficit | Forward minus reversed deficit |
| --- | ---: | --- | ---: | --- | --- |
| 1990–2004 | 198 | -32.4 (-39.7 to -28.6) | 175 | -35.2 (-43.8 to -31.3) | +2.8 (-1.0 to +9.5) |
| 2005–2019 | 76 | -29.1 (-39.6 to -18.8) | 80 | -30.7 (-40.3 to -22.7) | +1.6 (-6.7 to +12.0) |

Forward entries had positive indices in 33.6% and 41.8% of their five follow-up years. Matched controls had positive indices in 66.1% and 70.9%. Reversed entries gave 38.6% and 41.8%, against control values of 73.8% and 72.5%.

The mean future change in log(1 + index), relative to the origin year, was also lower for entries. Forward entry-minus-control contrasts were -0.589 and -0.553. Reversed contrasts were -0.744 and -0.573. The early forward-minus-reversed contrast was +0.155 (block range +0.009 to +0.387). Its species-resampling range included zero (-0.081 to +0.400). The late contrast was +0.020 (-0.206 to +0.321). Thus an early abundance-direction signal did not repeat clearly. These log contrasts are not annual population growth rates.

A second outcome was a positive index in at least three follow-up years. Its directional contrast was +8.7 percentage points early (+2.7 to +19.0) and +1.3 late (-10.5 to +12.1). The early result gives some evidence of directional change. It does not support a repeated direction across both periods. These outcomes and sensitivity checks are correlated. Their ranges are not adjusted for multiple comparisons.

## Design

An entry had a positive annual index after five consecutive explicit zero indices. The primary analysis kept the first qualifying entry per species-site pair, scanning from 1981 in the selected time direction. Only origins in 1990–2019 entered the reported cohorts. This definition includes reappearances. It does not assert first colonisation or local breeding.

A control had a positive index in the same calendar year, five valid prior indices and at least three prior positive indices. It was the same species, within 200 km, within 0.5 units of log(1 + origin index), and within a factor of two in transect length. We selected up to three controls by squared abundance difference and squared distance, after scaling by the two limits. We selected controls before checking future records. Controls could be reused. No entry site could be its own control.

For the main analysis, each retained entry and control needed five valid follow-up indices. We removed selected controls without this coverage, then gave the remaining controls equal weight for that entry. We gave entries equal weight. We did not replace excluded controls with new controls. All matching rules, including the reversed history and follow-up, were the same in both directions.

Only standard UKBMS transects in England, Scotland and Wales with public coordinates and positive reported length entered. We removed all 2,786 rows with repeated species-site-year keys. Missing rows and negative indices were never set to zero. Index -2 means that the sampling was not sufficient for a reliable index. Valid records covered 3,226 sites and 69,450 species-site pairs, with 593,932 non-negative annual records after the stated filters. Many pairs did not meet the entry rule.

The early forward cohort had 40 species at 99 sites; the late cohort had 19 species at 61 sites. The reversed cohorts had 37 species at 95 sites and 26 species at 60 sites. Mean matched distances were 94, 82, 95 and 81 km for early forward, late forward, early reversed and late reversed records. The initial abundance balance was close but not exact. Mean entry-minus-control log indices were -0.077, -0.051, -0.089 and -0.075 in the same order.

Selection was substantial. Early forward candidates fell from 795 eligible events to 516 with a match, then to 198 with complete entry and control outcomes. Late forward candidates fell from 308 to 253 to 76. The corresponding reversed counts were 646 to 490 to 175, and 886 to 711 to 80. Files/selection.csv gives every year. These samples describe continuing, well-recorded transects with matching support.

The plan was written before outcome calculations. After the first results, we added exact abundance matching, all qualifying events, and common-species checks. We also corrected the annual-trajectory denominator for the partial-follow-up sensitivity. The primary complete-case estimates did not change. The planned unadjusted contrast against all established records was not used; the reported raw means refer to matched records. This is an exploratory analysis, not a registered test.

## Why a matched deficit does not identify an establishment cost

Let each local population have a constant latent observation mean, lambda. Across populations, lambda has a Gamma distribution with shape a and rate b. Given lambda, all yearly counts are independent Poisson observations. This process has no population growth phase, no climate trend and no change in habitat. It has the same distribution when time runs backward.

If the current count is n and the previous k counts are zero, the posterior distribution of lambda is Gamma(a + n, b + k + 1). The expected next count is therefore:

`E[next count | current n, k prior zeros] = (a + n) / (b + k + 1)`.

Its probability of a positive next count is:

`1 - ((b + k + 1) / (b + k + 2)) ** (a + n)`.

For a = 0.5, b = 0.1, k = 5 and n = 1, these values are 0.246 and 0.204. For populations with the same current count of 1 but at least three positive counts in the previous five years, numerical integration gives 1.812 and 0.755. The persistence deficit is 55.1 percentage points. It is exactly the same in reversed time.

The different histories select different constant means, even after exact matching on the current count. This is a selection effect, not a slow establishment phase in this model. A simulation of 500,000 series checks the integration and the time symmetry. Files/stationary_null.py gives the proof calculation and simulation. The parameters were chosen as an example. The model was not fitted to UKBMS, does not reproduce its whole sampling process, and does not estimate how much of the observed deficit has this cause.

## Sensitivity and uncertainty

All results are in files/sensitivity.csv. Both time directions retained negative persistence and abundance contrasts after a tighter abundance limit, exact origin-index matching, migrant exclusion, three zero-history years, four positive-history control years, inclusion of all qualifying events, and restriction to species present in both directional samples. Under exact origin-index matching, the forward persistence deficits were -29.2 and -30.9 percentage points; reversed deficits were -31.1 and -36.5. Thus the main pattern is not due only to the small origin-index imbalance.

In warm-affinity species, the early directional persistence contrast was +9.6 points (+0.3 to +16.7), but the late contrast was -5.5 (-16.8 to +6.4). Affinity came from the frozen European index table in SCI 814f6d39, rather than a British index that can contain national decline patterns. The cut was the median across that table, 16.236 C. This subset has only 33 late forward entries and 38 reversed entries. It is not a test of a local warming effect.

Allowing at least three valid follow-up years kept negative entry-control deficits in both directions. The late directional point contrast changed sign. Restricting entry to the first positive record anywhere in the available past left only six late forward entries, so this check cannot support a later-period conclusion about new colonisation.

Spatial ranges resample entry-site blocks and hold matching and eligibility fixed. They do not fully propagate uncertainty from controls reused across different entry blocks. Species resampling keeps all observations of the same species together and gives a second view of dependence. Neither approach is a joint space-time detection model. Only 10 to 17 blocks contribute to the main single-direction estimates. The intervals can be unstable and do not cover all selection uncertainty.

## Scope and relation to other work

Core and transient species, and the effect of imperfect detection on that classification, are established topics (Snell Taylor et al., 2020). Finite records can also give different apparent colonisation and extinction times (Kuczynski et al., 2023). Xu et al. (2026) report many transient colonists and discuss regression to the mean in community abundance records. We do not claim that these general concerns are new.

The contribution is a matched forward-and-reversed test in British butterfly records, with a separate-period check and a closed-form counterexample for the exact history rule. It directly tests the establishment interpretation left open by the campaign turnover analysis (SCI 3f5200e4). It complements the source-distance recovery test (SCI 01dd32f0), which also states that recovery records do not identify dispersal limitation.

Time reversal is a diagnostic control. The empirical data need not be stationary or reversible. Changing climate, management, range position, monitoring and species composition can all alter the two directional samples. Similar contrasts do not prove equivalence or rule out establishment costs. The study lacks repeated-visit detection estimates, larval breeding records and measured habitat quality. An annual zero index is not proof of absence. Adults can visit a site without breeding there.

The result leaves a clear requirement for future attribution: a proposed establishment mechanism must explain more than the low abundance and persistence already selected by zero-history rules. A stronger test needs independently measured local breeding and survival, source populations and habitat, with detection estimated from repeated visits. We do not assign a fraction of the thermal-tracking gap to any process here.

## Rights and reproduction

The publication contains original code, narrative, figures and statistical aggregates. It does not contain raw UKBMS data, the frozen species-index table, or a record-level derivative database. Those inputs and panels stay in external scratch. Files/EXTERNAL_DATA.md gives full source citations, attribution, rights, URLs and version details. Files/provenance.json records the exact paths and SHA-256 hashes of all inputs used.

Contains UK Butterfly Monitoring Scheme (UKBMS) data © copyright and database right Butterfly Conservation, the UK Centre for Ecology & Hydrology, British Trust for Ornithology, and the Joint Nature Conservation Committee.

Follow files/REPRODUCE.md. The analysis takes less than a minute on the prepared research environment with one numerical-library thread. Run files/validate.py to inspect aggregate identities, the external panel, a synthetic time-reversal test, missing-value handling and the model simulation. All code and evidence needed for this analysis are preserved here or in the cited immutable SCI input publication.

## References

- Botham, M.S.; Middlebrook, I.; Harrower, C.A.; Milborrow, J.; Roy, D.B. (2025). United Kingdom Butterfly Monitoring Scheme: site indices 2024. NERC EDS Environmental Information Data Centre. https://doi.org/10.5285/53a1c705-4437-48bb-9bcd-b68977f8edd9
- Botham, M.S.; Middlebrook, I.; Heywood, J.; Harrower, C.A.; Milborrow, J.; Roy, D.B. (2025). United Kingdom Butterfly Monitoring Scheme: site location data 2024. NERC EDS Environmental Information Data Centre. https://doi.org/10.5285/d7256b49-f2e3-4ae7-907d-af729610c768
- Snell Taylor, S.; Coyle, J.R.; White, E.P.; Hurlbert, A.H. (2020). A simulation study of the use of temporal occupancy for identifying core and transient species. PLOS ONE 15, e0241198. https://doi.org/10.1371/journal.pone.0241198
- Kuczynski, L.; Ontiveros, V.J.; Hillebrand, H. (2023). Biodiversity time series are biased towards increasing species richness in changing environments. Nature Ecology & Evolution. https://doi.org/10.1038/s41559-023-02078-w
- Xu, W.; Gao, J.; Su, Q.; Lv, X.; Chase, J.M. (2026). Widespread declines of formerly common species reshape local assemblages over time. Nature Communications 17, 10769. https://doi.org/10.1038/s41467-026-77501-4
