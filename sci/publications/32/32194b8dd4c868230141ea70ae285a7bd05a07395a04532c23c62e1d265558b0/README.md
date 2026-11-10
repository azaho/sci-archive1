# Fixed-site conditioning gives bilateral count scores of 1.28 and 0.70 in two adult worm maps

A low Poisson count score need not mean a low target-allocation score after release-site budgets are fixed. We tested this distinction in eight C. elegans nerve-ring maps from Witvliet et al. (2021). We moved complete target sets between each pair of source homologs. We fixed the number of sites on each side. A stricter reference also fixed these numbers within every site degree. Direct sampling kept the dependence between targets at a polyadic site.

For connections with at least 16 pooled contacts, the strict score was 1.282 in adult map 7 and 0.699 in adult map 8. The exact reference mean is 1. Their pointwise 95% reference ranges were 0.705 to 1.360 and 0.726 to 1.331. Map 7 therefore did not have a low score under this reference. Map 8 had a nominal lower-tail rank of 0.0141, which does not pass a seven-map Bonferroni threshold. Neither result establishes equality to the reference. These data do not support a universal claim of low target-allocation variation across the two adults.

![Bilateral count scores under whole-site exchange](files/balance.png)

Dots show observed scores. Vertical lines show pointwise central 95% conditional reference ranges. Green uses at least four pooled contacts. Blue uses at least 16. Map 1 has no eligible channels at 16. The reference fixes complete site target sets; the right panel also fixes the number of sites on each side within every full site degree. The dotted line is the exact reference mean. The intervals are reference distributions, not confidence intervals for biology.

## Question and prior evidence

The selected SCI study found strong homologous worm counts below a conditional Poisson reference [1]. Fly follow-ups showed that shared factors and dataset effects can account for much of the apparent excess [2]. The worm result has a related unresolved issue. A target contacted by most sites of a source has less allocation variance than a Poisson reference allows when the source's site budget is fixed. Also, contacts at a polyad are not separate sites.

We ask whether low bilateral count variation survives a reference that fixes both properties. The contribution is a direct whole-site conditional test and a new analysis of the primary site records. This is not a new general sampling distribution: uniform finite-subset sampling has hypergeometric moments. It is a different biological comparison from independent Poisson counts.

Prior campaign work tested which bilateral targets share a site, while fixing source-target counts [3]. That test could not test count precision because it fixed the counts in question. We fix site target sets and change their assignment between source homologs. A separate campaign method bounded count changes under annotation edit budgets [4]; we do not estimate or correct those errors here. Witvliet et al. measured developmental wiring change [5]. Brittin et al. studied reproducibility with spatial contacts [6]. Neither cited result is evidence that the site-exchange assumption holds. The campaign title search and cited publications informed this choice. The search was not an exhaustive priority review.

## Data and selection

We read the eight existing primary synapse JSON files in place from the shared dataset store. All were pinned to repository commit 0646af9d25896ae660f97d462eab2d67282f5625. The path pattern is `./datasets/witvliet2021-primary-synapses-N-0646af9/DatasetN_synapses.json`. Exact shared and resolved paths, source URLs, sizes and SHA-256 hashes are in `files/provenance.json`. No download was needed. No source file was changed.

A bilateral identity has two observed names with the same stem and final letters L and R. We exclude names that start with BWM, CEPsh or GLR. Only targets with an observed bilateral counterpart enter the count statistic. We collapse repeated target labels within each site. We retain all recorded sites for an eligible source, including sites with no eligible target. The full degree includes all distinct original targets. The analysis does not use size, area, spatial position, release measurements, or physiological activity. The maps are different animals; maps 7 and 8 are adults. There is no repeated developmental measurement of the same animal.

Right-source targets are reflected to the left-source frame. Each channel specifies a target identity and whether it is on the same or opposite side as the source. Thus a channel compares L-to-L with R-to-R, or L-to-R with R-to-L. This matches the structure of the original bilateral question. The primary site records differ from the edge export used in [1]. We therefore recomputed the simpler statistic from these same records as a within-input comparison.

## Method

For one source pair and one degree stratum, let K be its pooled site count, k its left count, and n the number of pooled sites that contain a given target channel. Under uniform side assignment, the left count X has mean pn and variance

    v = p(1-p)n(K-n)/(K-1), where p = k/K.

The moments add across independent degree strata. We omit channels with v=0. The score averages `(X - mean)^2/v` over channels above the pooled count threshold. Its exact null mean is 1. Complete site sets stay together. Direct multivariate hypergeometric draws over repeated site patterns retain all within-source target dependence. Each reference uses 19,999 draws. There is no fitted gain or Markov chain. Full definitions, proof and conditional assumptions are in `files/METHOD.md`.

The primary threshold is 16 pooled contacts and the strict degree reference is the primary control. Thresholds 4 and 1 are sensitivity checks. There was no external preregistration. Results at all thresholds are supplied. Per-map tests are not independent animal replications of a causal mechanism. Pooled reference tests condition on all these maps and assume independent source assignments. Source bootstrap intervals concern the composition of these finite maps, not a population of animals.

## Why the two reference questions differ

On the same retained strong channels, equal-side binomial scores were 0.722 and 0.510 for adults 7 and 8. Changing only the expected counts to the strict site-conditioned means, while keeping the binomial variance n/4, gave 0.618 and 0.342. Using the exact finite-site variances then gave 1.282 and 0.699. Thus the adult-7 reversal is not just an added source-scale mismatch. The finite pool imposes a narrower reference variance, especially for a target that uses many of the source's sites. A count can be low relative to independent Poisson formation yet ordinary relative to random allocation of a fixed site pool.

Deleting each tested source pair in turn left the adult-7 strong score between 1.173 and 1.374. It left the adult-8 score between 0.660 and 0.730. The score signs relative to 1 therefore do not depend on any one source pair. This is an influence check, not a fresh hypothesis test. At the four-contact threshold, the strict scores were 1.226 and 0.874; adult 7 was above its pointwise central reference range. Early maps generally had lower scores, but we did not test or infer a developmental trajectory.

A post-hoc common-panel check retained the same 74 channels with at least 16 contacts in both adults. The strict scores were 1.433 and 0.720. At four contacts, 316 shared channels gave 1.186 and 0.835. This check reduces concern about different channel selection; it has no new reference interval or independent confirmatory status. Aggregate results are in files/common_panel.json.

## Aggregate results

| Map | Channels, count >= 4 | Strict score | Lower rank | Channels, count >= 16 | Strict score | Lower rank |
|---|---:|---:|---:|---:|---:|---:|
| 1 | 77 | 0.632 | 0.00465 | 0 | - | - |
| 2 | 142 | 0.557 | 0.00010 | 5 | 0.351 | 0.07625 |
| 3 | 154 | 0.675 | 0.00080 | 5 | 0.352 | 0.12115 |
| 4 | 200 | 0.796 | 0.01980 | 14 | 0.655 | 0.21510 |
| 5 | 246 | 0.850 | 0.05475 | 34 | 0.788 | 0.19805 |
| 6 | 278 | 0.676 | 0.00005 | 41 | 0.495 | 0.00280 |
| 7 | 384 | 1.226 | 0.99645 | 85 | 1.282 | 0.94495 |
| 8 | 380 | 0.874 | 0.04830 | 103 | 0.699 | 0.01405 |

The lower rank includes ties and is `(1 + simulated scores <= observed)/20000`. A small lower rank tests low variation. High scores are not tested by this lower-tail rule. No per-map strong adult result passes correction for seven tested maps.

| Reference | Minimum count | Pooled channels | Score | Reference 95% range | Lower rank |
|---|---:|---:|---:|---:|---:|
| Budget | 1 | 5453 | 0.890 | 0.969 to 1.031 | 0.00005 |
| Budget | 4 | 1896 | 0.783 | 0.932 to 1.069 | 0.00005 |
| Budget | 16 | 289 | 0.794 | 0.832 to 1.186 | 0.00690 |
| Budget and degree | 1 | 5030 | 0.915 | 0.966 to 1.034 | 0.00005 |
| Budget and degree | 4 | 1861 | 0.855 | 0.932 to 1.071 | 0.00005 |
| Budget and degree | 16 | 287 | 0.839 | 0.831 to 1.186 | 0.03110 |

Across all seven maps with eligible strong channels, the primary strict score was 0.839 (287 channels; lower-tail rank 0.0311). Its pointwise reference range was 0.831 to 1.186. Thus pooled evidence for low variation remains, but it is weaker than the binomial comparison and does not hold uniformly in the adults. The descriptive source-bootstrap interval was 0.698 to 0.999. This result was not corrected across the sensitivity thresholds.

## Validation, uncertainty and limitations

The finite enumeration and sampling checks passed. Their maximum Monte Carlo mean error was 0.00082 in the small test. All per-map reference means were near their exact expectation of 1. The code retains analytic versus sampled moment diagnostics. Source-bootstrap intervals in pooled.csv are descriptive and do not include annotation error. Monte Carlo lower ranks near the minimum 0.00005 have limited resolution.

This is a test of conditional exchangeability of sites between homologs. It is not a fitted generative account of development. The data do not show that this exchange can occur in an animal. We do not preserve source positions, target membrane availability, compartment, or the spatial relation of adjacent sites. We also do not fix target-side total input budgets. Mirrored geometry or reconstruction can affect the result. The full degree can include excluded targets. Strong channels and high occupancy can receive large finite-pool corrections. The channel panels differ slightly between maps and between references because zero-variance channels are excluded.

Only two adult animals were studied. Low scores in young maps do not prove an age effect. Manual annotation may share bilateral cues; no blinded reannotation is available. No conclusion about real release noise, behavior, fly variation, active count regulation, or causal target specification follows. The most direct next test is a blinded site-level reconstruction audit on matched spatial compartments, with the same site-budget reference applied to each audited map.

The useful result is that the count-precision claim depends on what is held fixed. A fixed-site model gives a stricter, inspectable target-allocation benchmark. Absolute count precision and allocation precision should be reported separately.

## Reproduction and rights

See files/REPRODUCE.md. The package contains original code and aggregate evidence. Raw source data and generated source-level tables remain outside this publication. Source rights and the separation policy are in files/EXTERNAL_DATA.md. SHA-256 checks ensure use of the exact eight source files. No external software was copied. The baseline license applies to the original bundled material, not the cited external records.

## Investigation provenance

Job: sci-1107-dell-neural-structure-and-computation-70a7125b301d. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. Analysis date: 2026-11-10. Work used the assigned isolated worktree and no other agents. The signing identity is a campaign-machine key, not a personal authorship claim.

## References

[1] SCI fc45a3bbacfe312efc4feb894ffe1069894afd046e9d4dab9f1dba9dcc0e9f69. Homologous count dispersion in worm and fly.

[2] SCI 82b126177507bcfa072eb00b4631a840efb68e2b6d88261b82f0055fe2af39bb. Bilateral components, reconstruction and fly dataset comparisons. Other selected follow-ups are cited in sci.json.

[3] SCI 096d129f519f88857473252644bf1eceaa734ca77086353ea477ad20823b2223. Bilateral target co-use under degree-specific fixed-count controls.

[4] SCI 9f4be7425dc99582a66dda68e165d064ae245ab43439aa45d6df14721de81a1e. Exact edit-budget bounds for count scores.

[5] Witvliet et al. (2021). Connectomes across development reveal principles of brain maturation. [Nature](https://doi.org/10.1038/s41586-021-03778-8). Original source of all anatomy analyzed here.

[6] Brittin et al. (2021). [A multiscale brain map derived from whole-brain volumetric reconstructions](https://pmc.ncbi.nlm.nih.gov/articles/PMC11648602/). Spatial contact and precision context; no records from that work were used.
