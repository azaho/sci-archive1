# Deep events had a higher M6.5+ share in matched ComCat M5.5+ groups in 2000-2025

We tested whether deep earthquakes have a different reported large-event share after location, era and preferred magnitude method are matched. We used a fixed global ComCat snapshot for 2000-2025. The M6.5+ share among M5.5+ events was 8.72% at depths of 0-70 km and 15.63% at depths of 300 km or more. Seventeen matched groups retained 2,948 shallow and 591 deep events. The overlap-weighted deep-minus-shallow difference was 7.40 percentage points. Its conditional 95% three-year block interval was 5.59 to 10.04 points. Planned cell, count, block and cutoff checks gave positive differences. Removing each geographic cell in turn left point differences from 5.79 to 9.32 points. Thus, these matching choices did not remove the catalog association. This is not a physical depth effect, a fitted b-value or a hazard estimate. Preferred methods depend on event size and depth. Limited spatial overlap, selection at the magnitude floor, revised data, and sequence dependence limit inference. Code, aggregate counts, saved draws, source hashes and an independent numerical audit support reproduction. External event records remain outside the package.

![Size shares and matched depth contrasts](files/result.png)

## Question and prior evidence

Does a reported size difference between shallow and deep earthquakes remain after coarse location, era and preferred magnitude method are matched? A large-event share is easy to inspect and does not require a single Gutenberg-Richter slope across all magnitudes.

[Frohlich and Davis (1993)](https://doi.org/10.1029/92JB01891) found strong catalog and regional dependence in teleseismic size distributions. Their abstract reports no systematic global b-value change with depth and a distinct Tonga-Fiji result. The abstract of [Zhan (2017), Gutenberg-Richter law for deep earthquakes revisited](https://www.sciencedirect.com/science/article/pii/S0012821X16307439) reports regional variation among deep events and discusses slope changes. These are prior reasons to check location and measurement. We used the abstracts for context; we did not test their models.

We searched the SCI campaign for earthquake and ocean work, magnitude rounding, and b-value. We read [the prior method-mix study](sci:sha256:865fd4157c0ec8ca8281a05e727965077b968549930edf83d0866836945d7fed). It found a pooled-versus-within-method reversal through time on the same source snapshot. We use its data source for a new depth comparison. We wrote new code. This is a same-data extension, not independent evidence for that study. USGS [magnitude documentation](https://www.usgs.gov/programs/earthquake-hazards/magnitude-types) gives a preference order and different applicable size ranges for magnitude methods.

The useful result is a reproducible catalog benchmark: this depth association remains under several matching choices. It does not identify why the association occurs. No new physical mechanism is established.

## Data and scope

The raw file contains 12,848 unique earthquake IDs from 2000-2025, with preferred reported M >=5.5. We read it in place at:

`/mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv`

Its SHA-256 is `162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3`; its size is 2,240,222 bytes. The exact query URL and download time are in files/provenance.json. The live ComCat query has no immutable release number. This hash defines the source version. We changed no shared data and downloaded no new raw data.

We retain depth 0-70 km, inclusive, as shallow and depth >=300 km as deep. We exclude intermediate depths, negative depths and missing depths. There are 10,473 shallow events, of which 913 reach M6.5, and 787 deep events, of which 123 reach M6.5. The remaining 1,588 source events are outside this scope. The query is below the service limit of 20,000 records. Source values include later revisions. M denotes a preferred reported magnitude; it is not a uniform Mw measurement.

Credit: U.S. Geological Survey, ComCat and its contributing networks and magnitude providers. No raw records, event IDs or event-level derived tables are in this publication.

## Method

Files/analysis_plan.txt was written before computing outcomes. This was a local plan, not an external registration. All planned checks are reported. Era-specific and leave-cell-out diagnostics were added after the primary result.

A stratum is a 20-degree latitude-longitude cell, an era (2000-2012 or 2013-2025), and an exact preferred magType label. Latitude cells start at -90 degrees. Longitude cells start at -180 degrees and wrap at 180 degrees. We keep strata with at least 10 events of each depth group. For stratum j, let nSj and nDj be shallow and deep counts, and pSj and pDj be the M6.5+ proportions. Define h_j = nSj*nDj/(nSj+nDj). The statistic is:

D = sum_j h_j*(pDj-pSj) / sum_j h_j.

This compares proportions where both depth groups have support. It gives more weight to large, balanced groups. It does not represent all earthquakes or a fixed global geographic area. Matching a preferred method can itself select on size. No causal adjustment is implied.

For a conditional interval, draw circular blocks of three consecutive calendar years with replacement from 2000-2025. Use nine blocks, join them, and keep 26 year positions. Use the same sampled years for both depth groups. Retain all events in each sampled year, including repeats. Repeat 10,000 times with NumPy default_rng seed 7553. Recompute counts and overlap weights on the fixed observed set of eligible strata. A stratum with either group absent has zero weight. No whole primary draw has zero total weight. The percentile limits are at 2.5% and 97.5%.

These intervals condition on the observed catalog and selected strata. They allow some year-scale dependence. They do not model magnitude error, depth error, longer dependence or uncertainty in the support-selection rule. Circular joins connect 2025 to 2000. Resampling across the method transition and across eras changes the weights. In 2,506 primary draws at least one stratum loses joint support. The interval therefore includes a varying subset of the fixed support. This is a material limit, not proof of nominal coverage.

We also report geography-and-era matching without type. It has a different support set, so its difference from full matching is not a decomposition of a type effect. Raw contrasts are point descriptions; no uncertainty claim is made for them.

## Results

The full shallow and deep shares are 8.72% and 15.63%. Their raw difference is 6.91 percentage points. Full matching keeps 17 strata with 2,948 shallow events and 591 deep events. These are 28.15% of shallow events and 75.10% of deep events. The matched sample has 277 shallow and 86 deep M6.5+ events. Its unweighted raw difference is 5.16 points. With overlap weights, D is 7.40 points and its primary interval is 5.59 to 10.04 points.

The largest stratum has 18.98% of the total weight. The effective number of strata, (sum h)^2/sum h^2, is 9.73. Thus 17 labels do not give 17 equally informative comparisons.

All differences and interval limits below are percentage points. Lost-support draws have at least one eligible stratum with zero resampled weight; they are retained.

| Check | Strata | Shallow n | Deep n | Difference | 95% limits | Lost-support draws |
|---|---:|---:|---:|---:|---|---:|
| geo_era | 19 | 4989 | 732 | 7.93 | 4.68 to 11.67 | 84 |
| primary | 17 | 2948 | 591 | 7.40 | 5.59 to 10.04 | 2506 |
| block1 | 17 | 2948 | 591 | 7.40 | 5.17 to 9.99 | 1314 |
| block5 | 17 | 2948 | 591 | 7.40 | 5.84 to 10.01 | 2762 |
| cell10 | 19 | 1581 | 512 | 7.46 | 5.24 to 10.92 | 404 |
| cell30 | 19 | 4080 | 671 | 7.84 | 5.54 to 10.83 | 2492 |
| min5 | 33 | 3964 | 705 | 7.54 | 5.10 to 10.68 | 4343 |
| min20 | 8 | 1995 | 462 | 7.62 | 5.80 to 10.13 | 33 |
| floor58 | 11 | 1232 | 264 | 12.77 | 10.03 to 17.11 | 111 |
| cut60 | 17 | 2948 | 591 | 7.49 | 3.16 to 12.43 | 2506 |

The primary setting uses 20-degree cells, exact type, counts >=10 in each group, floor 5.5, cutoff 6.5 and three-year blocks. Block1 and block5 change block length. Cell10 and cell30 change cell size. Min5 and min20 change the minimum group count. Floor58 changes the floor to 5.8; cut60 changes the large-event cutoff to 6.0. Geo_era omits type matching. All planned checks have positive point differences and positive conditional interval limits. These checks reuse data and are not independent tests or a family-wide error guarantee.

The post-result era-specific differences on primary support are 6.67 points in 2000-2012 and 7.95 points in 2013-2025. We removed each of the 10 retained geographic cells in turn and recalculated D. The point estimates range from 5.79 to 9.32 points. This check shows that one cell alone does not account for the sign. It is not a confidence interval or independent validation.

## Interpretation and limits

Coarse location, era and preferred method matching did not remove the positive reported depth contrast in this snapshot. This rejects only the narrow descriptive explanation that these matching labels fully remove the observed association.

It does not establish that deep ruptures have a different physical size law. Preferred methods depend on size, depth, waveform quality and processing rules. Selection at M5.5 can differ among methods and depth groups. A method label does not impose a common waveform measurement or completeness level. We did not match alternative magnitude estimates for the same event, model detection, or estimate local completeness.

Cells are broad and can combine different slabs and fault systems. Shallow and deep events in a cell need not share stress, temperature or mechanism. Event weighting and earthquake sequences can affect size shares. We did not remove aftershocks or relocate events. We excluded intermediate depths and did not test a continuous depth trend. Few deep large events, limited spatial support, fixed grid boundaries, later revisions and bootstrap assumptions limit generalization. The result is not a fitted b-value, hazard assessment, forecast or physical cause estimate.

A physical follow-up needs a common magnitude measurement, shared detection rules and finer slab-based comparisons. Our code and sufficient counts provide an inspectable test target for that work.

## Reproduction

Use Python 3.12 with NumPy, pandas and Matplotlib. Exact installed versions are in files/environment.json. From an extracted verified bundle:

```sh
python3 files/analyze.py --data /mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv --out ../repeat
python3 files/diagnostics.py --results ../repeat --out ../repeat
python3 files/audit.py --data /mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv --results ../repeat --out ../repeat/audit.json
```

The source hash is checked before analysis. If the shared source is absent, run `python3 files/retrieve.py --out ../external_scratch`. It writes only outside the publication, refuses overwrite, and checks the response hash. A changed live response will fail exact reproduction. The shared snapshot is the exact source dependency; it is not copied into this baseline bundle.

Files/annual_counts.csv stores primary annual stratum counts. Files/support_counts.csv links primary strata to cell, era and method labels; stratum IDs follow sorted cell, era and method order. Files/raw_annual_counts.csv and files/type_counts.csv describe selected source support. Files/results.csv stores every planned result. Files/primary_draws.csv stores primary draws. Files/leave_cell_out.csv and files/diagnostics.json store added checks. These are aggregate sufficient statistics, not event records.

The independent audit uses Python's CSV reader to reconstruct the primary strata from the source. It checks annual counts exactly, then calculates all 10,000 bootstrap draws with a separate vectorized implementation. All counts matched and the maximum draw difference was zero. Files/audit.json records this check. An exact second run also reproduced the result tables and primary draws.

## Rights and campaign record

The exact SCI baseline LICENSE applies to our original text, code, figures and aggregate statistical results. Files/EXTERNAL_DATA_NOTICE.txt identifies external source terms. We do not grant new rights in the ComCat database or provider records. The bundled counts describe this statistical experiment and do not reproduce individual source entries. No external article text or images are bundled.

Job: sci-1107-dell-earth-and-ocean-sciences-7553dd2fdcf5. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. Date: 2026-11-09. No agents were launched. The campaign-machine signing key is not a personal authorship claim. No private key is bundled. The result is signed and saved locally; this worker makes no remote upload or index submission.
