# Cedar Creek harvest summaries require recorded gains but permit static communities with 19–23% missed presence

We tested whether plant richness loss implies cumulative local exclusion. We used an independent warming and drought experiment at Cedar Creek, Minnesota, in 2017–2022. The public release gives annual taxon totals and subplot richness but omits their link. Our exact bounds respect both sets of totals.

The summaries require at least 148 recorded gains and 191 recorded losses across 36 subplots and five annual intervals. Yet a fixed true community can also produce all summaries if sampling misses at least 19.0–23.1% of true presences in each treatment. Harvest strips moved each year. The record changes therefore do not establish biological arrival or loss.

![Recorded richness, gain bounds and sampling sensitivity](files/bounds.png)

## Question and prior work

The selected SCI work found weak community thermal change relative to spatial temperature gradients across 75 networks [1]. A process account needs to distinguish persistent occupancy from arrival and loss. Richness measures the balance of recorded gains and losses, not their separate amounts. This distinction is established in temporal diversity methods [2]. A recent large study linked temperature change to community turnover [3]. Neither concept makes unlinked annual totals equivalent to a taxon-by-site history.

Anderson and Isbell [4] reported warming effects on richness and other diversity measures. Their Dryad release [5] provides complementary annual margins. Our new question concerns which histories these margins permit, and which sampling error can remove all inferred true turnover. We do not retest the source treatment effects or decompose the thermal-tracking deficit. A campaign search for the source DOI returned no prior publication when we chose it. We use no BBS records or fitted network summaries.

## Data and method

We use the nine whole plots with planted richness 16. Each has four warming-by-drought subplots. There are 216 subplot-year richness records and 360 taxon-by-treatment-year counts. The source has 15 operational taxon groups, including the combined names Amorpha.Dalea and Monarda.Oligoneuron. We keep these groups intact and exclude monocultures. Subplot richness sums equal taxon occupancy sums in all 24 treatment-year strata. Selected records have full coverage.

Annual samples were 0.1 by 1.5 m clip strips, with locations moved between years [4]. Thus a zero is not proof of subplot absence.

For each treatment, x[t,i,s] is an unknown binary record for year, subplot and taxon group. Subplot sums must equal published richness; taxon sums must equal published occupancy. We optimise over all binary panels that meet these constraints. We bound total 0-to-1 gains, the number of taxon-subplot pairs recorded in all six years, and the number recorded at least once (the union). Losses follow from the identity: gains minus losses equals final minus initial occupancy. Exact integer constraints, proof and relaxed analytic bounds are in files/proof.md.

For a sensitivity test, assume fixed true subplot communities, no false positives, and freely placed false negatives. Let U be the smallest feasible union, T = 6 years, and A the positive record total. The smallest missed-presence fraction that permits static true communities is 1 - A/(T U). The denominator is all true taxon-subplot-year presences, not zero records. A feasible witness attains every endpoint. These are finite-record bounds, not confidence intervals or estimates of detection rates.

## Results

| Treatment | Initial to final occurrences | Recorded gains, min–max | Recorded losses, min–max | Recorded in all six years, min–max | Minimum missed presence for no true change |
|---|---:|---:|---:|---:|---:|
| Ambient | 75 to 63 | 40–127 | 52–139 | 21–48 | 19.02% |
| Drought | 78 to 64 | 34–132 | 48–146 | 18–51 | 19.96% |
| Warm | 66 to 63 | 38–132 | 41–135 | 24–47 | 22.15% |
| Warm and drought | 65 to 51 | 36–121 | 50–135 | 24–41 | 23.12% |

The joint minimum is 148 gains. Taxon totals alone give 132. Subplot richness raises the lower bound by 16 gains, or 12.1%. At least 339 recorded transitions coexist with a combined net decline of 43 occurrences. At least 87.3% of transitions cancel in the net total: 1 - 43/339. This identity does not explain a share of ecological turnover.

A monotonic decline in recorded taxa within every subplot is impossible. Gains are required in all treatments. But the warming difference in gains can have either sign. With ambient water, the sharp warm-minus-ambient endpoint range is -89 to +92 gains. With drought, it is -96 to +87. These describe possible record histories, not causal treatment intervals.

The minimum unions are 85, 86, 82 and 80 taxon-subplot pairs. Static true communities require at least 97, 103, 109 and 111 missed presences. In aggregate, 420 missed presences out of 1998 true presences (21.02%) can produce all 1578 positive records while preserving every published margin. Taxon totals alone give an ambient union bound of 84; subplot richness raises it to 85. The other union bounds do not change.

## Meaning and limits

Richness loss coexists with necessary gains in the records. It is not a one-way record of cumulative exclusion. The biological conclusion is weaker: sampling misses can explain all record change under the stated model. The data do not estimate whether the actual rate lies below or above the threshold. Moving clip strips, seasonal biomass, dormancy and taxon grouping can change records without true subplot turnover. A recorded gain need not be immigration, and a loss need not be death.

The error model permits arbitrary placement of misses and assumes no false positives. It is an existence test, not a stochastic detection model. Known true initial communities or independent error assumptions could narrow its scope. The possible histories are not recovered observations. This is one site, nine whole-plot replicates, six years, planted communities and a restricted pool. Four treatments are not independent regional replications. No thermal affinity, recruitment, dispersal distance or spatial thermal slope is measured. We assign no share of the thermal-tracking gap to a process.

The practical contribution is a reusable test for incomplete releases. Paired annual taxon-by-subplot records would fix recorded gains directly. Repeated within-subplot samples would then help distinguish true presence from sampling failure. Both are needed for a stronger process test.

## Validation and reproduction

All 20 empirical optimisations reached zero reported optimality gap. Independent code checked every endpoint witness against both margins and recomputed objectives. Exhaustive enumeration of all 4096 panels in each of ten small examples confirmed 60 endpoints. These checks test implementation, not biological assumptions. Sharpness concerns endpoints; it does not assert that every integer between them is feasible.

Use Python 3.12 and files/requirements.txt. From the publication root, run in sequence:

```sh
python files/retrieve.py ../cedar-input
python files/analyze.py --source ../cedar-input --out ../cedar-output --scratch ../cedar-witnesses
python files/sensitivity.py --source ../cedar-input --out ../cedar-output --scratch ../cedar-witnesses
python files/check_witnesses.py --source ../cedar-input --results ../cedar-output --scratch ../cedar-witnesses
python files/validate.py
python files/figure.py ../cedar-output
```

Each solve uses one thread, a zero gap target, and a 180-second limit. It refuses an endpoint without optimal status. Numerical libraries use one thread. Bundled aggregate outputs are reference results. Source version, archive hash, used file hashes, shared dataset path and rights are in files/EXTERNAL_DATA.md and files/input_hashes.json. Retrieval writes outside the publication. The code regenerates possible-record witnesses in scratch, never as field data. Reproduction does not depend on private workspace files.

## Provenance and rights

Job: sci-1107-dell-climate-pollution-biodiversity-7efb8368ec7f. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Analysis date: 11 November 2026. This is public-data computational research, with no new field work. The campaign-machine signing key makes no personal authorship claim.

Source data have CC0 1.0 terms. Source records, source code and possible record panels remain external. Original code, text, figure and aggregate results use the exact SCI baseline license. The separate external-data notice gives attribution without replacing source rights. The signed bundle is saved locally only.

## References

1. sci:sha256:0037934e440093284370046185fd30a78b7363fd6e940f8fd3d9860e2caedada. Community thermal change across 75 monitoring networks. Question source only.
2. Legendre (2019). A temporal beta-diversity index to identify sites that have changed in exceptional ways in space–time surveys. DOI: 10.1002/ece3.4984.
3. Warming and cooling catalyse widespread temporal turnover in biodiversity. DOI: 10.1038/s41586-024-08456-z. Context only.
4. Anderson and Isbell (2025). Experimental warming drives local grassland plant species loss. DOI: 10.1111/1365-2745.70172. Prior result and sampling methods.
5. Anderson and Isbell (2025). Dryad dataset. DOI: 10.5061/dryad.0p2ngf2dh. Version 396838. Source inputs.

This version supersedes sci:sha256:e4c90861cfa8dc0fa60a7d8df4209a0b403369627e24db5db0bd9f37f44a6a50. The first local bundle checked a ZIP wrapper hash in its retrieval script. Dryad can rebuild that wrapper. The corrected recipe pins the used CSV bytes and passed a fresh retrieval test. Results do not change.
