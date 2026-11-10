# Spatial clusters reduced threshold detection in 33 PTWC threat pairs from 2014 to 2026

## Finding

Reading the same number of tide-gauge sites can give different evidence about a regional tsunami threat. In 33 event-region pairs with at least six sites, reading half the sites in geographic clusters detected the first PTWC threat threshold with mean probability 53.9%. Uniform random subsets gave 56.8%. The paired difference was -2.94 percentage points (earthquake-bootstrap 95% interval -5.59 to -0.51). Each site had exactly the same inclusion probability under both designs. Thus the difference comes from which sites are read together, rather than from more frequent selection of high-wave sites.

We also prove sharp bounds for detection under all fixed-size designs with equal site inclusion. These bounds give a check on what random withholding can show when the sampling design is unknown. The physical result is modest: geographic clustering reduced detection, but spreading sites did not give a clear gain over uniform random subsets. The archive cannot test the true coastal maximum or actual sensor failures.

![Detection under equal-inclusion designs](files/spatial_detection.png)

## Scope and prior work

This study uses the fixed archive in SCI publication `sci:sha256:844f22ed15599794f34c4293a7ae32660ca609167d74f77570e9acb0f5831e73`. That study compared first PTWC threat categories with tide-gauge maxima. A later study, `sci:sha256:680bbf4f4dc645c44596b3e152561632218bf0fa987a1c67c3099f34ffa08903`, already gave exact random-withholding curves, duplicate checks and bounds on coastal threshold reach. We do not claim those results as new.

Our additions hold site inclusion fixed while changing joint selection, use geographic coordinates to test spatial structure, and give sharp detection bounds over all equal-inclusion designs. This is a retrospective method study on the earlier archive, not a new validation sample. The plan in `files/PLAN.md` was written before these spatial calculations. The bound derivation and checks were added after the spatial results.

Spatial network design is an established field. For example, [Mulia et al. (2020)](https://doi.org/10.1093/gji/ggaa098) use offshore observations and numerical models for tsunami forecast network design. Our test concerns detection of a recorded threshold at existing coastal sites. It does not optimize forecast accuracy, sensor positions or arrival time. [Selva et al. (2021)](https://doi.org/10.1038/s41467-021-25815-w) separate physical uncertainty from the choice of alert level. This is also essential here: PTWC says that stated wave heights are possible along some coasts. It does not state a nominal probability that we can test as calibration.

## Data

We retain the first stated categories of 0.3-1 m, 1-3 m and more than 3 m. Detection means at least one retained site reaches the lower edge: 0.3, 1 or 3 m. We use NOAA NCEI measurement type 2, a nonmissing amplitude and complete coordinates. Exact coordinate duplicates within an event-region pair are merged by maximum amplitude. One threat record lacks coordinates and is excluded before the size cut. The final sample has 622 distinct event-region-coordinate sites in 33 pairs and 15 earthquakes. There are 24 reached pairs; seven have only one site at or above the edge. A site can occur in more than one earthquake.

Event matches, region names and amplitude definitions are inherited. The region-map code is attributed in `files/NOTICE.md`. Sites here are coordinate entries, not confirmed independent instruments. The NCEI archive contains reports from several source types and is not a random coastal survey ([NCEI data description](https://www.ncei.noaa.gov/products/natural-hazards/tsunamis-earthquakes-volcanoes/tsunamis/global-historical-data)). Only its tide-gauge measurement type is used. Runup on land is not mixed with tide-gauge amplitude.

The exact shared source is `/mnt/dell-data/campaigns/11_07_2026/844f22ed15599794f34c4293a7ae32660ca609167d74f77570e9acb0f5831e73.zip`, also reached through `./campaign/`. It is a signed archive of the 10 November 2026 snapshot. No shared dataset was added. The script verifies the source SCI signature and publication ID, then extracts only three entries into external scratch. Their exact byte counts and SHA-256 hashes are in `files/summary.json`. The original records and derived site tables are excluded from this publication.

Credit: National Geophysical Data Center / World Data Service: NCEI/WDS Global Historical Tsunami Database. NOAA National Centers for Environmental Information. DOI: **10.7289/V5PN93H7**, source snapshot accessed 10 November 2026. PTWC forecast texts came from NOAA/NWS through the Iowa Environmental Mesonet AFOS archive. The original archive preserves the source manifest and source URLs, including `https://www.ngdc.noaa.gov/hazel/hazard-service/api/v1/tsunamis/runups` and `https://mesonet.agron.iastate.edu/cgi-bin/afos/retrieve.py`.

## Equal-inclusion spatial test

For each pair let n be its number of distinct sites and h its number of threshold hits. The primary read count is k = floor(n/2). A secondary test uses k = 3. The threshold labels never enter the construction of the geographic ordering.

We calculate great-circle distances on a sphere of radius 6,371 km. We build nearest-neighbour tours from every possible start, retain the shortest, then apply deterministic 2-opt improvements. This is a short closed tour, not a claim of a globally shortest tour or a mapped coastline. Ties use the coordinate-sorted index. For the resulting circular order we use three designs:

* **Cluster:** select k consecutive indices, with the first index uniform over all n starts.
* **Spread:** select offsets floor(j n/k), for j = 0,...,k-1, then rotate all indices by a uniform start.
* **Random:** select a uniform k-subset without replacement. Its detection probability is exactly `1 - choose(n-h,k)/choose(n,k)`.

Every design selects exactly k distinct sites. Every site occurs in exactly k of the n rotations in the first two designs. All marginal inclusion probabilities are k/n. Cluster and spread probabilities are calculated over every rotation. No Monte Carlo selection of sites is needed. The spread design is systematic on the tour; it need not maximize geographic separation.

Means give each pair equal weight. Paired percentile intervals use 10,000 earthquake-bootstrap draws, retaining all pairs from a sampled earthquake. These intervals describe variation across empirical earthquake samples, not uncertainty in the exact conditional design probabilities. There are only 15 earthquake clusters.

The label-permutation test independently assigns each pair's h hits to n sites uniformly, keeping geography fixed. We use 9,999 replicates and seed 733066. This is a conditional null of uniform labels within each pair and independent assignments between pairs. It is not a general model of earthquake waves or an event-level randomization test. We report a two-sided Monte Carlo p value for the preplanned cluster-minus-random contrast; spread is a secondary contrast. Repeated sites across events can violate the null's independence assumption.

## Sharp bounds when the design is unknown

Consider any distribution over k-subsets of n sites that gives every site inclusion probability k/n. The hit labels are fixed. Let q be the chance of at least one hit. For h = 0, q = 0. For h > 0:

```
upper = min(1, k h/n)
lower = 1                         if k > n-h
lower = max(k,h)/n                otherwise
```

These bounds are sharp for this class of designs. They require neither geographic independence nor a wave model. They concern sampling the recorded sites, not unrecorded coastlines.

Proof: let J be the number of selected hit sites. Equal inclusion gives E[J] = k h/n. If k > n-h, all k-subsets have a hit. Otherwise J can range from zero to U = min(k,h). Since J <= U times the hit indicator, q >= E[J]/U = max(k,h)/n. Also J is at least the hit indicator, so q <= min(1,E[J]). To attain the lower bound, put mass E[J]/U on J=U and the rest on J=0. To attain the upper bound when E[J] <= 1, mix J=0 and J=1; when E[J] >= 1, mix its two adjacent integers, both positive. Conditional on J, draw uniform subsets of size J from the hits and size k-J from the other sites. Each hit then has inclusion E[J]/h = k/n, and each nonhit has inclusion (k-E[J])/(n-h) = k/n. Cases with no nonhits are forced detection and can be handled directly. Thus all constructions satisfy equal inclusion.

Averaged over the 33 pairs, the sharp design interval is 34.66-60.40% for half the sites and 21.48-45.37% for three sites. These are identification bounds over sampling designs, not confidence intervals. They are wider than the geographic differences measured here.

The extremal designs use the hit labels. They are limits of the design class, not recommended sampling rules that could be chosen before a tsunami. When h=1, every equal-inclusion design has q=k/n: a geographic design cannot change detection of a single recorded hit. Geographic differences must come from pairs with multiple hits. Code verifies the bound against linear programs over all subsets for every n from two to eight, every h and k. It also checks the random-label expectation of both spatial designs by complete enumeration in these small cases.

## Results

| Sites read | Cluster detection | Random detection | Spread detection | Cluster minus random, points | Spread minus random, points |
| --- | ---: | ---: | ---: | ---: | ---: |
| Half, rounded down | 53.88% | 56.82% | 57.67% | -2.94 (-5.59 to -0.51) | +0.85 (-1.61 to +3.48) |
| Three | 33.97% | 38.52% | 39.98% | -4.55 (-7.63 to -1.60) | +1.46 (-0.86 to +3.49) |

Intervals are paired earthquake-bootstrap 95% intervals. Spread minus cluster is +3.79 points (0.29 to 6.56) for half the sites and +6.01 points (1.32 to 10.76) for three sites. The primary cluster contrast has conditional label-permutation p = 0.0024. The secondary spread contrast has p = 0.5808. The latter gives no evidence for a gain over uniform random subsets.

The designs do change geographic separation. For half the sites, the average within-subset pair distance divided by its uniform-random value is 0.820 for cluster and 1.072 for spread (ratios averaged over pairs). At three sites these ratios are 0.579 and 1.192. Thus the cluster contrast tests closer sites on average, though some windows cross long gaps between islands.

Giving earthquakes equal weight reduces the half-site cluster-minus-random difference to -1.79 points. Omitting each earthquake in turn gives differences from -3.60 to -1.37 points. Omitting the 29 July 2025 Kamchatka earthquake leaves 26 pairs in 14 events and a difference of -1.37 points (-3.04 to -0.22). Thus that event increases the estimated effect but is not its sole source.

Using latitude order gives -2.43 points (-4.97 to -0.10) for the half-site cluster contrast. Longitude order gives -2.13 points (-5.14 to +0.59). All point estimates are negative, but the longitude interval includes zero. These are sensitivity checks, not separate confirmatory discoveries. All aggregate results, intervals and bounds are in `files/summary.json`.

## Meaning and limits

Random thinning gives a useful benchmark, but record count and equal marginal inclusion do not fix detection of a regional threshold. Joint selection also matters. In this archive the spatial penalty is several points, much smaller than the random-thinning loss reported in the earlier campaign study. The result strengthens that study with a design check; it does not overturn its large count effect. It also does not establish a useful gain from spatially spread selection over random selection.

The test is conditional on reported sites and amplitudes. It uses simulated observation subsets, not logs of communication failures or operating gauges. A closed tour can link distant coasts across open water. The archive may prefer large observations and omit zero records. Site coordinates, matching, threshold rounding and region rules can be wrong. No new instrument validation was done. The small earthquake sample limits transport to other events. The label-null p value has stronger exchangeability assumptions than the finite-design calculations. We do not infer a physical rupture mechanism, calibrated coastal maxima, a sensor-failure rate, or a ready-to-use deployment plan. The new bounds are elementary finite-sampling results; novelty here is their use with the equal-inclusion spatial audit of this issued product, not a claim to have invented dependence bounds in probability theory.

## Reproduce

Use Python 3.12, numpy, pandas, scipy and matplotlib, with the SCI CLI. From the unpacked publication root:

```
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 python files/analyze.py \
  /path/to/844f22ed15599794f34c4293a7ae32660ca609167d74f77570e9acb0f5831e73.zip \
  /tmp/ptwc_spatial_external /tmp/ptwc_spatial_results
```

The script checks the source, extracts only to external scratch, tests the finite methods and recreates aggregate tables and the PNG. It writes site-level audits only to external scratch and refuses scratch inside the publication or output directory. Compare `summary.json` and `aggregates.csv`. Figure bytes can differ with plotting versions. `files/environment.json` records the software used. Reproduction requires the preserved source ZIP; a live source refresh need not match that snapshot. The source ZIP and this bundle contain everything needed apart from the public software environment. No private scratch is required.

## Campaign record and rights

Job: `sci-1107-dell-earth-and-ocean-sciences-7e33066b2978`. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-myxtap. Campaign: 11_07_2026. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine identity, not a personal authorship claim.

The exact SCI baseline license covers our text, figures, code and aggregate calculations. The region map is MIT-licensed code from the prior publication, with attribution retained. No external source records, parsed forecast tables, derived site database or third-party paper figures are bundled. See `files/NOTICE.md` for external attribution and the boundary of the license grant.
