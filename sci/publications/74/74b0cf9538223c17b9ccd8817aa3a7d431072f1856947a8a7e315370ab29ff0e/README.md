# Twelve of 85 M3+ events in an Oklahoma box in 2021-2025 followed two years without a detected M2.5+ event within 5 km

Job: `sci-1107-dell-earth-and-ocean-sciences-244263020d8c`. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Analysis date: 2026-11-10. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

We test two spatial constraints on the residual earthquake rate after the Oklahoma disposal cuts. First, does the later activity occupy a different spatial distribution? Second, how often does a later M3+ event occur after a long local gap in detected events?

In a fixed ComCat snapshot, the box 34-37 N, 99.6-95.9 W contains 85 M3+ events in the five full years 2021-2025. Of these, 64 (75.3%) are within 5 km of a 2010-2016 M3+ epicentre. The median distance is 0.71 km. This agrees with earlier evidence that residual events often revisit the earlier earthquake footprint. It does not show that they rupture the same fault plane.

Twelve of the 85 events (14.1%) follow more than two years with no detected M2.5+ event within 5 km. Five follow more than five years. With a 10 km radius, seven follow more than two years and three follow more than five years. Thus, a short fitted clustering taper and a long local quiet period can coexist with later activity. Quiet at this detection threshold is not evidence of permanent local cessation.

The main spatial comparison does not resolve a distribution change between 2014-2016 and 2021-2025 (exact year-map permutation p = 17/56 = 0.304 at 10 km kernel scale). This null is not evidence of spatial equivalence. It also does not identify the physical driver of the residual rate or distinguish pore pressure, stress transfer, and later operations.

![Spatial distribution and annual shares](files/results/spatial.png)

![Local quiet periods](files/results/quiet.png)

## Prior work and added evidence

The six selected SCI studies report a faster decline than pressure forecasts, a residual rate above the old level, short fitted ETAS clustering, and a weak relation between taper and background rate. SCI 76c63172 already reports that residual epicentres are close to earlier events. We do not claim to discover that persistence. Our added evidence is a catalog-based measure of local detected quiet periods, and a spatial comparison that treats years, rather than individual earthquakes, as permutation units.

Campaign searches for Oklahoma and spatial recovery were made before this analysis. We also read the later SCI studies c1b51c6e, aab4f008, and 5a909384. They show limits to the inverse-rate duration interpretation, limits to magnitude-order tests, and the difference between a direct offspring taper and whole-sequence completion. Our local-gap statistic is none of those durations. It measures what the catalog recorded before an event at a specified radius and magnitude threshold.

Prior research establishes that injection depth and volume reductions can both affect rates (Skoumal et al., 2024, doi:10.1785/0320240030). This makes a spatial check useful, but the present analysis contains no well-operation data. The spatial kernel statistic follows the maximum mean discrepancy method of Gretton et al. (2012). The statistic and its year-level use are specified below. Neither general method nor the idea of fault reactivation is new. The contribution is a reproducible, bounded test of these constraints in the residual period.

## Data and fixed scope

We reuse this shared raw dataset in place:

```
./datasets/comcat-oklahoma-m2p0-2010-20261110/comcat-oklahoma-m2p0-2010-20261110.csv
```

Source: USGS ComCat preferred event solutions, downloaded on 2026-11-10. The CSV has SHA-256 `03f5cb719126e70499d17faad121cbbee32e3b9a538a62f6ddc6ee1bd0190b01`, size 2,136,814 bytes. `files/provenance.json` records the exact query and resolved shared path. No raw download was needed. ComCat is mutable; a new query can return revised solutions.

We retain type earthquake, coordinates inside 34-37 N and 99.6-95.9 W, and magnitudes rounded to one decimal. There are 12,231 M2+ source rows in this box. The main target threshold is M3.0. We use full years 2014-2016 for the peak comparison and 2021-2025 for the late comparison. We exclude partial 2026 from inference. Earlier events from 2010 provide local history. This box is not the full state. It excludes southern Kansas and parts of eastern Oklahoma. We do not extend counts to the full state or to the full 2021-2026 interval in earlier papers.

We do not remove aftershocks or assign triggering ancestry. This avoids using a fitted ETAS taper to test the same taper. Coordinates use a local plane: latitude scale 111.195 km per degree; longitude scale multiplied by cos(35.5 degrees). Distances are epicentral, not hypocentral or fault distances.

## Methods

**Spatial comparison.** For each of the eight selected years, form the empirical spatial distribution with total mass one. Thus, a year with 887 earthquakes and a year with six each have one unit of mass. For years i and j, compute

```
K_ij = mean over all event pairs of exp[-distance_squared/(2 h_squared)]
T = v_transpose K v
v_i = 1/3 in 2014-2016; -1/5 in 2021-2025.
```

Within-year means include diagonal pairs. T is the squared distance between mean annual kernel maps. The main h is 10 km. We enumerate all 56 choices of three of the eight years as the first group. The upper-tail p value includes the observed assignment. `primary_permutations.csv` preserves all 56 statistics.

The tested null is exchangeability of the annual empirical maps. It permits any clustering within a year. It does not establish exchangeability between years. Cross-year sequences, serial trends, and unequal precision due to unequal counts can violate it. This is a conditional reference test, not a causal treatment test or an exact test of all possible uniform-thinning processes. The coarse permutation resolution and only three peak years limit power. We retain the original squared-mean statistic and do not select a more favorable statistic after seeing its null result.

We also report h = 5 and 20 km, M2.5+ and M3.5+, and exclusion of a 20 km circle centred at 35.53 N, 96.75 W near Prague. These are sensitivity checks, not independent confirmation. No family correction is applied across these checks; isolated small p values cannot establish a general shift. An empty annual M3.5+ group after the circle removal makes that comparison undefined; its entries are blank, not zero p values.

**Footprint distance.** For each late event, find the nearest 2010-2016 event at the same magnitude threshold. We report the empirical distance quantiles and fractions within fixed radii. A large reference catalog makes short nearest distances more likely, so this is a descriptive footprint measure. It is not a random-location significance test, a matched-count test, or proof of common fault identity.

**Local quiet period.** For each 2021-2025 M3+ event, find the last earlier detected M2.5+ event within 2, 5, or 10 km. Use all events from 2010 onward, including earlier events in the late period. The target itself and simultaneous records are excluded by a strict time inequality. There is no sequence selection, ancestry fit, or look-ahead. If no earlier event exists, the gap is left censored at the start of 2010. All such lower bounds exceed five years, so these targets count above all tabulated thresholds. The code uses infinity as a censor flag, not as a measured infinite gap. It does not include event-level outputs in the publication.

The local-gap analysis was added after the spatial null was seen. It is exploratory. No event-independent confidence interval is given because targets can share sequences. These fractions describe events, not probabilities of restart per fault, per quiet area, or per monitoring site. Such probabilities require a denominator of all eligible quiet sites and exposure time.

## Results

### Local quiet periods

Targets are the same 85 M3+ events in each row. History is detected M2.5+ activity.

| Radius | Median gap, days | Gap over 1 year | Gap over 2 years | Gap over 5 years | No earlier detected neighbour since 2010 |
| --- | ---: | ---: | ---: | ---: | ---: |
| 2 km | 32.1 | 27 | 17 | 9 | 5 |
| 5 km | 32.1 | 25 | 12 | 5 | 1 |
| 10 km | 28.9 | 22 | 7 | 3 | 0 |

Using M3+ instead of M2.5+ for the earlier history increases the 5 km count above two quiet years from 12 to 26 and the median gap from 32 to 162 days. The term quiet is therefore strongly threshold dependent. Even M2.5+ history does not measure all fault activity. Smaller events, aseismic slip, and undetected events can occur during these intervals.

### Spatial persistence and comparison

For M3+, 68.2% of late events are within 2 km of the 2010-2016 footprint, 75.3% within 5 km, and 85.9% within 10 km. The 90th percentile distance is 13.3 km. At M2.5+, 79.7% lie within 5 km of the earlier M2.5+ footprint. Short distances are common, but not universal.

| Threshold | Kernel scale | Year-map p value | With Prague circle removed |
| --- | ---: | ---: | ---: |
| M3+ | 5 km | 0.304 | 0.982 |
| M3+ | 10 km | 0.304 | 0.964 |
| M3+ | 20 km | 0.214 | 0.821 |
| M2.5+ | 5 km | 0.214 | 0.679 |
| M2.5+ | 10 km | 0.054 | 0.286 |
| M2.5+ | 20 km | 0.018 | 0.018 |

The M2.5+ 20 km result is scale dependent and uncorrected across the tested choices. It does not override the M3+ main null. M3.5+ without circle removal gives p = 0.84-0.93. At M3+, the fraction west of 97.5 W is 0.44, 0.61, and 0.59 in the three peak years, and 0.91, 0.85, 0.42, 0.42, and 0.17 in the five late years. The late distribution varies strongly by year. Pooled maps can hide this variation.

The event-weighted yearly rates in the two broad longitude regions fell to 2.59% (west) and 2.19% (east) of their respective 2014-2016 rates. This descriptive split was not optimized. It gives no simple broad eastward movement of the residual activity over the whole late period.

## Interpretation and limits

The evidence supports a narrow joint statement: much residual activity is close to earlier activity, while some residual events follow several years without a detected nearby event. Local detected silence and spatial persistence are compatible. Neither establishes a continuing external driver by itself. A delayed response, a new external perturbation, earthquake interactions, and an unobserved sequence of small events can each contribute.

The main spatial null does not show that every local region declined by the same factor. It also does not show that a single physical driver continued on all faults. A field test of the driver needs well depth and operation histories, reservoir pressure or deformation, and a justified matched spatial design. The quiet-period counts provide concrete target conditions for such a test. The source snapshot, code and exact definitions allow them to be regenerated without fitting a triggering kernel.

Catalog magnitude practices, mixed magnitude types, location error, and changes in detection can alter both distances and gaps. The 2 km results are especially sensitive to location error. History before 2010 is absent. The M2.5 threshold is a sensitivity choice, not a completeness proof for every place and year. We use one catalog, so this is not an independent OGS-ComCat replication. The local-gap statistic does not estimate ETAS duration, the duration of a whole family, or the fraction of events caused by external forcing. No new physical cause of the short taper is identified.

## Validation and reproduction

An independent dense-matrix calculation reproduces the main spatial statistic and all 56 permutation comparisons. A separate brute-force radius calculation reproduces the 5 km median and the count of 12 gaps above two years. A known one-day interval checks time units explicitly. `files/results/audit.json` records the arithmetic checks. The final complete script was run again into separate scratch and its aggregate outputs were compared. The checks cannot validate catalog completeness or the exchangeability assumption.

Python versions are in `files/results/summary.json`. Required packages are NumPy, pandas 3.x, SciPy and Matplotlib. No service or special environment is needed. After verifying and extracting the publication to a new folder, use a separate scratch output directory:

```sh
python files/code/analyze.py --input /path/to/shared/comcat-oklahoma-m2p0-2010-20261110.csv --out /path/to/scratch/results
python files/code/audit.py --input /path/to/shared/comcat-oklahoma-m2p0-2010-20261110.csv --results /path/to/scratch/results
```

The analysis requires the stated hash. If the shared snapshot is unavailable, `python files/code/fetch.py --scratch /path/to/external/scratch` repeats the source query and records its hash outside the publication. It stops if ComCat has changed. Exact reproduction then requires the retained shared snapshot; the query alone cannot promise a historical catalog version. The aggregate evidence in the package remains inspectable without it.

No raw catalog, selected event table or derivative record database is bundled. The package contains our code, text, aggregate tables, figures and provenance. Source terms and attribution are in `files/EXTERNAL_DATA_NOTICE.md`. These materials can use the SCI baseline license without replacing external terms.

## References

The SCI metadata cites all six selected publications and the three later campaign results discussed above. External sources used are:

- USGS ComCat event service: https://earthquake.usgs.gov/fdsnws/event/1/
- USGS copyrights and credits: https://www.usgs.gov/information-policies-and-instructions/copyrights-and-credits
- Skoumal, Barbour, Rubenstein and Glasgow (2024). Reduced injection rates and shallower depths mitigated induced seismicity in Oklahoma. doi:10.1785/0320240030. We read the USGS publication summary.
- Gretton et al. (2012). A Kernel Two-Sample Test. Journal of Machine Learning Research 13, 723-773. https://www.jmlr.org/papers/v13/gretton12a.html
