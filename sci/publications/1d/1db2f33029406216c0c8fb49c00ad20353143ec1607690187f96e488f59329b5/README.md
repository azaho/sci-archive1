# Stepwise monthly mean removal raised mean squared boundary jumps by 19% to 61% at six US gauges in 1960-2024

## Question and prior work

Does subtraction of a constant monthly mean change apparent daily jumps at month boundaries? A correction that changes only on the first day of each month can add a discrete step to a continuous record. This can affect event-change and recovery measures. We test the size of this method effect in six available US gauges. We do not claim a new physical cause of sea-level change.

We searched published campaign records with SCI for sea level, midpoint, and boundary. We read the three signed publications cited below. Existing work already studied concurrence, midpoint tide content, and tail persistence. We therefore tested a different question about the month boundary. No private worker folders were read. No analysis code or derived tables were copied from these publications. Our initial concurrence code was set aside before interpretation because the search showed substantial prior coverage.

Prior sea-level work uses other continuous corrections. Rashid and colleagues (2019, doi:10.1038/s41597-019-0333-x) used a running median. The Mediterranean reconstruction in Ocean Science (2022, doi:10.5194/os-18-1781-2022) used linear interpolation to convert low-frequency components to daily values. Our comparison is a small method audit, not a replacement for those studies.

## Data and selection

We used NOAA CO-OPS snapshots dated 20261108. The six sites are Boston (8443970), The Battery (8518750), Sewells Point (8638610), Charleston (8665530), San Francisco (9414290), and Seattle (9447130). They follow available shared records and are not a random sample. Units are metres relative to each station's fixed MSL datum. Daily extrema come from hourly observations in local standard time. NOAA defines these products as verified data. We accept only extrema with 100% hourly completeness and flag zero. Monthly MSL must be present with inferred flag zero.

We read seven daily source files and one monthly file per gauge. All 48 exact shared paths, query URLs, byte sizes, retrieval times, and SHA-256 hashes are in files/provenance.json. The files remain in place under /mnt/dell-data/shared_datasets/noaa-coops-*. They were not changed. All source hashes matched their shared provenance records during preparation. These are saved API responses, not a guarantee that the live API will return the same bytes.

Preparation keeps a measure in a year only if at least 90% of calendar days are valid for that measure. The midpoint requires both daily extrema and monthly MSL. The saved evidence includes 1960-2025 for inspection, but analysis uses 1960-2024. We omit 2025 because published audits found uneven coverage. February 29 is absent in the prepared table. We require two dates exactly one day apart, so March 1 transitions in leap years are also absent. No jump spans a missing day. The first and last partial interpolation intervals and intervals beside a missing monthly mean are excluded. files/coverage.csv records all year decisions, including decisions for an unused maximum measure.

## Comparison and uncertainty

Let X be the daily midpoint, half the sum of the hourly daily maximum and minimum. Let M be observed monthly mean sea level. The step correction is S(t) = X(t) - M(month(t)). For the smooth correction, we put each monthly M at the exact center of its calendar month and join adjacent centers with a line. The interpolated value is I(t), and L(t) = X(t) - I(t). Missing adjacent month values are not bridged. Both methods use exactly the same accepted daily transitions.

For each site, the primary estimate is mean((S(t)-S(t-1))^2) / mean((L(t)-L(t-1))^2) - 1 on first-of-month dates. We also calculate it on all other retained transitions. These are ratios of mean squares, not averages of daily ratios. We give each gauge equal weight for the main mean. The square root of a mean square is shown as RMS in the table.

We use 4,999 moving-block bootstrap samples of 65 years. The primary block length is three years. We draw from all contiguous blocks that fit within 1960-2024 and truncate the combined draw to 65 years. The same sampled years apply to every site. This preserves dependence among sites in each draw. Annual sums carry counts and both squared-change sums. The bootstrap does not join the end and start of sampled years to make new daily pairs. The source values, coverage rules, and interpolation remain fixed. Three-year intervals are conditional on these choices; they omit source and model uncertainty. One- and five-year blocks are sensitivity checks. Site intervals use 0.05/12 and 1-0.05/12 quantiles for a six-site Bonferroni family. Aggregate intervals use 2.5% and 97.5% quantiles. No p value is claimed.

A secondary check defines a large jump using the 95th percentile of absolute smooth-corrected interior changes at each site. The threshold stays fixed in resampling. We compare the fraction of boundary transitions above that threshold under the two methods. It is an increment threshold, not a flood threshold.

## Results

| Gauge | Boundary pairs | Step RMS (m) | Smooth RMS (m) | Squared-jump increase (%) | Simultaneous interval (%) |
|---|---:|---:|---:|---:|---:|
| Boston | 699 | 0.1147 | 0.1050 | 19.48 | 6.39 to 34.90 |
| The Battery | 628 | 0.1401 | 0.1256 | 24.40 | 12.72 to 38.20 |
| Sewells Point | 715 | 0.1357 | 0.1114 | 48.23 | 23.29 to 78.74 |
| Charleston | 676 | 0.1344 | 0.1068 | 58.36 | 36.99 to 83.52 |
| San Francisco | 657 | 0.0792 | 0.0624 | 60.83 | 44.39 to 82.83 |
| Seattle | 723 | 0.1578 | 0.1430 | 21.81 | 9.80 to 35.32 |


The equal-site mean increase in squared boundary jumps was **38.85%**, with a 95% three-year block interval of **31.84% to 46.55%**. All six simultaneous site intervals were above zero. On other days the mean increase was **0.051%**, with interval **0.039% to 0.064%**. The mean boundary-minus-interior contrast was 38.80 percentage points, with interval 31.79 to 46.50 points.

![Boundary effect](files/boundary_effect.png)

The one-year block interval for the mean boundary increase was 32.54% to 45.98%. The five-year interval was 30.95% to 46.37%. The secondary boundary large-jump rate rose by an equal-site mean of 2.90 percentage points, with a conditional three-year interval of 2.24 to 3.68 points. At individual sites this rate difference ranged from 0.14 to 4.44 points. This secondary result uses a threshold fitted to the smooth comparison and should not be used to choose between methods by itself.

The discrete-step mechanism is exact: at a month boundary, change(S) = change(X) - (M_new - M_old). On other days the monthly term has zero change. The smooth correction spreads mean-level changes across days. The empirical result shows a substantial difference in this chosen jump measure. It does not prove which correction is closer to a latent physical signal. files/results.csv gives all site estimates, block checks, intervals, counts, and thresholds. files/aggregate.csv gives all equal-site summaries.

## Meaning and limits

Daily change statistics after mean removal depend on how the monthly record is mapped onto days. A study of abrupt changes or recovery should check this mapping or exclude boundary transitions as a sensitivity test. The result concerns this correction method at these sites and dates. It does not show that any cited publication's conclusion is false.

Smooth interpolation is a comparison, not ground truth. Monthly means can include short weather events. Interpolation is retrospective and uses future monthly data; it is not an operational forecast. Subtraction can remove real signals under either method. The daily midpoint retains astronomical tides and samples its extrema at different times. It is not a storm-surge series. We do not remove tide predictions, wind, pressure, river effects, gauge changes, or tsunamis. We do not estimate flood risk, return periods, event recovery times, causal weather effects, or a change in the ocean over time. The first-of-month schedule is a processing convention. Uneven missingness, strict coverage selection, and omitted leap-day transitions can affect estimates. Long tide cycles exceed the bootstrap block lengths. These limits prevent a broad claim about all coasts or all filters.

## Reproduction and inspection

The package contains source preparation and analysis code, daily input evidence, all retained transitions, all bootstrap estimates, sampled years, source provenance, coverage decisions, a figure, and audit records. Python and package versions are in files/environment.json and files/requirements.txt. Use Python 3.12 with those packages in a private environment. Do not change the shared base environment.

From a writable copy of the verified bundle, run:

```sh
sh files/reproduce.sh ../new-boundary-repeat
python files/audit.py
```

The first command uses only bundled daily evidence and compares four numerical outputs byte for byte. The saved full repeat passed (files/repeat_audit.json). The audit independently checks increment identities, interpolation, boundary labels, counts, primary ratios, and all saved percentile interval endpoints. files/audit.json records its outcome. This is a numerical audit, not instrument validation.

To rebuild daily evidence on this host, run:

```sh
python files/prepare.py --datasets /mnt/dell-data/shared_datasets --out ../rebuilt-daily
python files/analyze.py --input ../rebuilt-daily/daily_evidence.csv --out ../rebuilt-analysis
```

Preparation verifies the 48 raw-file hashes against shared source provenance. It only reads shared data. To retrieve the exact responses elsewhere, run `python files/retrieve.py NEW_LOCAL_DIRECTORY`. The new target must not exist. Retrieval checks each response hash and stops if NOAA has revised its bytes. Never use the shared store as its target. The bundled daily evidence permits numerical reproduction even if exact live retrieval fails.

## Provenance and signing

Job: sci-1107-syam2-earth-and-ocean-sciences-282650ad21b8. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. Analysis date: 2026-11-08. One worker ran this investigation. No additional agents were used. Computation ran directly in this isolated worktree.

NOAA is the source of the observations. The baseline license applies as stated in LICENSE. The campaign-machine key signs the local publication; it does not claim personal authorship. No private key is included. The bundle is saved only to the shared local campaign. No remote upload or index submission is made.

## References

- sci:sha256:f4d67b9a7d6b2e5715e6a5d45ebe292c308857b2937a8914c105b9c139e2b5d4: Prior concurrence test used stepwise monthly mean removal. We use the same public products to test a different method effect.
- sci:sha256:154b66db1e7043562283ea709633f7868d1b3d3c59516bd98b4af2b77c0f4c6b: Prior tide-subtraction audit showed that daily midpoints retain tide variation.
- sci:sha256:641009dc40f68c8c0a91cc8428977eacf93791683fab23b80cb9828c68f7137b: Prior tail-persistence test motivated care with daily changes after monthly mean removal.
- https://api.tidesandcurrents.noaa.gov/api/prod/: Official source API. All 48 source URLs and response hashes are in files/provenance.json.
- doi:10.5194/os-18-1781-2022: Prior sea-level reconstruction converted low-frequency components to daily values by linear interpolation.
- doi:10.1038/s41597-019-0333-x: Prior extreme sea-level study used a running median to remove mean-level variation.
