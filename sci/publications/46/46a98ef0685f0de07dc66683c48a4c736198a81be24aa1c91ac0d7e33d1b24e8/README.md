# The M4+ share stayed near 1 percent in a north Oklahoma–south Kansas box, but the 2020–2025 sample was small

Job `sci-1107-dell-earth-and-ocean-sciences-e6db5840f4ad`. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort, through Codex in T3 Code. Date: 2026-11-10. The signing key is a campaign-machine key. It does not state personal authorship.

## Result

We test a possible cause of the residual earthquake rate after the Oklahoma disposal cuts. A published model proposed that dense wastewater can move down through basement rock and increase pressure after injection falls. The study linked depth to earthquake size and suggested that large-event rates could fall more slowly. We extend a test of this size signature through 2025 in the exact box used for that study's size analysis.

In the current USGS ComCat snapshot, the box contains 2,996 M2.5+ earthquakes in 2013–2018 and 103 in 2020–2025. Both periods have six full years. There are 28 and one M4+ events. Thus the M4+ share is 0.935% and 0.971%, a ratio of 1.039. The conditional odds ratio has an exact event-independent 95% interval of 0.025–6.416. The data do not resolve M4+ enrichment. They also do not exclude a large increase in that share. The result is a limit on evidence, not proof that brine transport is absent.

The smaller M3.5+ threshold gives a share ratio of 1.385. Its interpretation depends on the reference test. The event-independent interval includes no change; a year-label test gives a small upper-tail reference fraction. We retain both results. This threshold does not establish the physical driver.

The depth part of the proposed signature needs separate care. Median preferred depth rises from 5.63 to 7.00 km, but median reported depth error falls from 5.9 to 0.4 km. The preferred network field has no `ok` entries in the early period and 92 of 103 in the late period. A direct comparison of these preferred solutions cannot isolate migration from changes in the catalog or in the active locations.

![Rate, size and depth audit](files/results/evidence.png)

## Question and prior work

The six selected SCI studies found rapid rate decline after the disposal cuts, residual activity above older levels, short fitted ETAS clustering, and weak dependence of taper on background rate. These observations do not select a unique pressure or stress process. The campaign also contains tests of nonstationary rate-state response, a joint productivity constraint, and local spatial persistence. We searched the campaign for Oklahoma and for Oklahoma magnitude density before this study. We read the selected work and these related results. We do not repeat their ETAS fits or their spatial tests.

Pollyea et al. (2019, doi:10.1038/s41467-019-11029-8) proposed a density-driven pressure process. Their model allows pressure to persist at depth after disposal cuts. Their Figure 5 used a size-depth relation to motivate slower decline of large earthquakes. We test a consequence in their stated box with later data. We do not test their flow equations or reproduce their 2019 catalog snapshot. A constant size distribution would not falsify every density-driven model: stress, faults, depth and the size law can each vary. Conversely, enrichment would not uniquely support brine transport.

The new contribution is a later-period, fixed-box size-ratio audit with a depth-quality check and explicit uncertainty. It separates decline in earthquake numbers from a change in size mix. It also shows what the current preferred-solution catalog cannot settle. It does not explain why the ETAS taper is short.

## Scope and source

The box is 36.125–37.235 N, 99.602–97.800 W. It includes north Oklahoma and south Kansas. It is not all Oklahoma. The time windows are 2013–2018 and 2020–2025, with 2019 left as a transition year. The first window matches the published size-depth study; the second consists of six full years after its publication year. This is a literature-led extension, not a prospectively registered test: we saw a broad Oklahoma pilot before choosing the exact published box and we inspected its totals before final analysis. No alternative box was selected for a larger effect. The 2013–2018 comparison includes both growth and decline, not a single peak-rate state. Full 2025 has zero M2.5+ records in this snapshot and box. Partial 2026 is excluded.

Final source, reused in place after download with the campaign dataset helper:

`./datasets/comcat-pollyea2019-box-m25-2013-2025-20261110/catalog.csv`

Resolved shared path, query, time, byte size and SHA-256 are in `files/provenance.json`. The source has 3,142 records including 43 in 2019, and SHA-256 `cb9ad385d21ed2fda43eee8efbba11dab060702d4e8dd569956af4073cc4313e`. It was retrieved on 2026-11-10. We did not read the failed HDD. The preliminary broad-box dataset and its hash are also recorded. Only the final snapshot enters the tables and figure.

ComCat combines preferred solutions from different networks. It is mutable. We select earthquake type, retain the stated boundaries, and round magnitude to one decimal before thresholds. We do not convert magnitude scales, remove aftershocks, fit a b-value, or infer ancestry. M3+ denominators and magnitude-type subsets check some sensitivity to detection and scale practice. They do not prove completeness or supply a homogeneous moment-magnitude catalog.

## Methods

For each period we count N events above a base threshold and K above a higher threshold. The size share is K/N. Its late/early ratio equals the ratio of the two rate declines, since periods have equal duration. This cancellation avoids interpreting the overall count fall as a change in size distribution. The primary high threshold is M4 and the primary base is M2.5. We also report M3.5 and a base of M3. These checks are related and not independent replications.

We use the two-by-two table [late high, late low; early high, early low]. SciPy supplies Fisher's two-sided p value and the conditional maximum-likelihood odds ratio with its exact 95% interval. An odds ratio is not a share ratio. These intervals assume independent event marks and no catalog bias. Sequences can violate that assumption. We therefore do not call them general physical confidence bounds.

Two further calculations show sensitivity to temporal units. We enumerate all 924 assignments of six of the 12 years to an early group. The statistic is late pooled share minus early pooled share, and the reference fraction includes the observed assignment. This requires exchangeable annual marked count maps. Years have very unequal counts and different network practice; chronological rate change and sequences across years can violate exchangeability. The fraction is a reference calculation, not a causal or distribution-free p value. We also resample six whole years within each period 10,000 times, retaining all events in each selected year. The percentile interval shows variation across the observed years; only six years per period limit its coverage. Zero late counts are retained. These tests were added after the totals were seen.

For depth, we tabulate reported depth and depth error, preferred network, and exact values of 5 and 7 km. Those exact values are diagnostic only; we do not assert that each is a fixed-depth solution. As a sensitivity scenario, form the envelope depth plus or minus twice the reported depth error. We count envelopes wholly below 8 km depth, wholly at or above 8 km, and those that cross the threshold or lack an error. These are not calibrated confidence intervals: network error definitions and biases can differ. They expose how much the depth classification depends on treating a preferred point estimate as exact. Depth-error filters of 2 and 1 km provide further descriptive tables. Such filtering changes the population and cannot recover the true depth effect by itself.

## Aggregate results

| Base | Higher threshold | Early K/N | Late K/N | Share ratio | Exact odds-ratio interval |
|---|---|---|---|---:|---|
| M2.5 | M4 | 28/2996 | 1/103 | 1.039 | 0.025–6.416 |
| M2.5 | M3.5 | 210/2996 | 10/103 | 1.385 | 0.652–2.796 |
| M3 | M4 | 28/934 | 1/37 | 0.902 | 0.021–5.767 |
| M3 | M3.5 | 210/934 | 10/37 | 1.202 | 0.542–2.775 |

The M2.5+ rate falls from 499.3 to 17.2 per year, or to 3.44% of its earlier value. The M4+ rate falls from 4.67 to 0.167 per year, or to 3.57%. These descriptive falls are nearly equal. A single late M4+ event makes the size comparison weak. The M3.5+ rate falls to 4.76% of its earlier value. It may decline less rapidly, but that statement does not extend to M4+ with useful precision.

For M4/M2.5, Fisher p is 1.00, the year-label enrichment fraction is 432/924 = 0.468, and the within-period year bootstrap share-ratio interval is 0–5.04. For M3.5/M2.5, the corresponding values are 0.325, 9/924 = 0.00974, and 0.50–2.37. The small year-label fraction is not suppressed. It tests a different and restrictive exchangeability null and does not establish a robust increase across the analyses. With M3 as the base, the M3.5 year-label fraction is 0.137. Complete values are in `magnitude_tests.csv`.

Magnitude type matters. In the ML-only subset the early and late counts are 2,638 and 92, with 122 and seven M3.5+ events, but four and zero M4+ events. In the moment-type subset (mwr or mww), the totals are only 141 and three. Those subsets are selected by magnitude reporting and cannot be treated as unbiased replications. A homogeneous waveform-based magnitude analysis is needed before a small size-law change can support a mechanism.

There are 157 nominal 8+ km events early and eight late. The early depth-error median is greater than the 1.37 km median-depth increase. With a two-error envelope, only four early records and two late records lie wholly at depths of 8 km or more; 2,905 early and 51 late records remain unresolved across that boundary or lack a reported error. The envelope audit and precision-filter counts are in `depth_quality.csv`. These envelopes do not measure a true deep fraction. In the early catalog the unfiltered depth–M3.5 table has 18 high events among 157 nominal deep events versus 192 among 2,839 shallower events (Fisher p = 0.035 under independent marks). With reported error at most 2 km and positive, only nine early deep events remain, of which one is M3.5+. The late deep group has eight events and none M3.5+. This is loss of information under a precision filter, not evidence that the earlier relation was false.

## Limits and implications

The outcome is a bounded null for the M4 size signature, with a tentative M3.5 pattern. The data cannot establish or exclude density-driven pressure as the residual driver. They do not show the absence of large-event hazard, a safe disposal limit, or the return to a natural rate. They do not measure pressure, salinity, well operations, or aseismic slip.

The data contain only one late M4+ event in this specific box. Other Oklahoma sequences, including Prague in 2024, are outside it. One must not apply this null to the full state. Changes in magnitude type, reporting network, location methods, detection, active fault populations and catalog revision can each affect the comparison. The depth-error fields cannot capture every systematic error. Annual blocks may split long sequences. The 2019 model did not specify a numerical future enrichment factor, so this is a signature test, not a calibrated forecast score.

A useful next measurement is a common relocation and magnitude procedure across both periods, followed by a joint test of size, depth and measured loading in the published box. Independent constraints on brine density and basement pressure would be needed for causal attribution. A successful total-count forecast is not enough to validate that mechanism; size and depth predictions need their own tests.

## Reproduce and inspect

The package contains code, aggregate tables, a figure and provenance, but no earthquake record table or external derivative database. Our text, code, figures and aggregate results can use the SCI baseline license. Source records remain external. `files/EXTERNAL_DATA_NOTICE.md` identifies them and preserves attribution.

With Python 3.12, NumPy, pandas, SciPy and Matplotlib, extract a verified publication into a new folder. Use the retained shared snapshot and an output directory outside the signed draft:

```
python files/code/analyze.py --input /path/to/datasets/comcat-pollyea2019-box-m25-2013-2025-20261110/catalog.csv --out /path/to/scratch/results
python files/code/audit.py --input /path/to/datasets/comcat-pollyea2019-box-m25-2013-2025-20261110/catalog.csv --results /path/to/scratch/results
```

`analyze.py` checks the exact source hash and records library versions. `audit.py` independently counts period totals using the Python CSV reader and checks the primary Fisher calculation by direct hypergeometric enumeration. No stochastic fit is used. Year bootstrap seed is 1107. All calculations run locally without a service.

If the snapshot is unavailable, `python files/code/fetch.py --scratch /path/to/external/scratch` repeats the precise query. It stops if the returned hash has changed and leaves the new bytes in scratch. Exact regeneration then requires the retained shared snapshot. Aggregate evidence remains inspectable without it. The source 2019 paper used an older snapshot; our early totals are not a claim of exact reproduction of its historical data.

## References

- Pollyea, Chapman, Jayne and Wu (2019). High density oilfield wastewater disposal causes deeper, stronger, and more persistent earthquakes. Nature Communications 10, 3077. doi:10.1038/s41467-019-11029-8. Published box and tested physical signature.
- USGS ComCat event service: https://earthquake.usgs.gov/fdsnws/event/1/ . Catalog source.
- USGS ComCat documentation: https://www.usgs.gov/programs/earthquake-hazards/anss-comprehensive-earthquake-catalog-comcat-documentation . Field definitions.
- USGS depth reference FAQ: https://www.usgs.gov/faqs/what-reference-datum-used-earthquake-depths . Network differences and depth limits.
- USGS copyrights and credits: https://www.usgs.gov/information-policies-and-instructions/copyrights-and-credits . Source terms.
- The six selected SCI studies and related campaign tests are cited by full ID in sci.json.
