# A weekly phase from 1984-2004 gave no clear positive transfer to Geysers M2+ earthquakes in 2005-2025

A weekly phase fitted to early Geysers earthquake counts did not clearly repeat in later years. The test projection was -3.87%, with a conditional 95% year interval of -8.33% to +0.79%. The two-sided month-shift test gave p = 0.0766. This result does not prove that weekly forcing is absent. It gives a fixed-phase test of one catalog pattern across time.

![Weekly rates and transfer scores](files/weekly.png)

Figure 1. Left: daily rates for each weekday, divided by the unweighted mean of the seven weekday rates. These raw rates are descriptive and do not have the month adjustment used in the test. Right: test projections along the phase fitted only in the training period. Lines give conditional 95% year bootstrap intervals. Each site and magnitude check fits its own training phase. The year-shift check also changes the calendar adjustment to whole years.

## Question and prior work

Does a weekly pattern in early geothermal earthquake counts keep its phase in later years? A repeatable weekly pattern could guide a test of human activity or catalog detection. It would not by itself establish either cause.

Trugman et al. (2016, doi:10.1002/2015JB012510) compared background and triggered rates at The Geysers, Coso and Salton Sea. They found different links to monthly injection among the sites. Atef et al. (2009, doi:10.1785/0120080217) linked apparent weekly and daily patterns in small western US earthquakes to changes in detection from human noise. Holmgren et al. (2026, doi:10.1038/s41598-026-38146-x) used a local Coso catalog and daily operation data to study seasonal injection and rapid seismic response. Their study does not test transfer of a calendar-week phase. These works motivate controls for detection, clustering and changes over time. We do not use their numerical data or repeat their mechanism tests.

The campaign result [SCI 0786c7b0...](sci:sha256:0786c7b0f49a750144031f8f6bad271c32e2ae172a7b265cc87f7bac29fdcd23) found no clear global UTC weekend contrast for M5.5+ events in 2000-2025. We read its signed text and use its month-rotation idea, with new code. Our local M2+ geothermal samples, fitted harmonic phase, and later-period transfer test differ from that global weekend test. We searched the campaign for earthquake, ocean, streamflow drought, deep earthquake, earthquake time rounding, earthquake geothermal weekly and Geysers. We found no exact precursor to this test. Search is limited by its terms and the available record. This is a scoped catalog test, not a first claim about weekly seismicity.

## Data and scope

We reused three shared ComCat snapshots retrieved on 10 November 2026. No download was needed. All raw files remain external. Exact source queries, file sizes, source and metadata SHA-256 hashes, worktree paths and resolved shared paths are in [provenance.json](files/provenance.json). Stable shared names are:

- `/mnt/dell-data/shared_datasets/comcat-geysers-m2p0-1984-20261110/comcat-geysers-m2p0-1984-20261110.csv`
- `/mnt/dell-data/shared_datasets/comcat-coso-m1p5-1984-20261110/comcat-coso-m1p5-1984-20261110.csv`
- `/mnt/dell-data/shared_datasets/comcat-saltonsea-m1p5-1984-20261110/comcat-saltonsea-m1p5-1984-20261110.csv`

These are query snapshots, not numbered releases. The source boxes are 38.70-38.90 N, 122.95-122.65 W for Geysers; 35.95-36.15 N, 117.90-117.70 W for Coso; and 33.10-33.25 N, 115.70-115.50 W for Salton Sea. The source floor is M2 for Geysers and M1.5 for the other two sites. All tests use M2 or higher. No depth filter or declustering is used. Boxes can contain tectonic events and need not match exact reservoir limits. Preferred magnitudes can use different scales. A magnitude cut does not prove complete detection.

The primary calendar uses fixed UTC minus eight hours. Training covers full local days from 2 January 1984 through 31 December 2004. Omitting 1 January avoids a partial local day at the source query start. Testing covers 1 January 2005 through 31 December 2025. A check uses America/Los_Angeles civil dates, including daylight saving time. Day counts use equal date weights; civil days can have 23 or 25 hours. With these full-year periods each weekday has equal total hours to very close approximation. No 2026 event is used. All zero-event days are included.

Credit: USGS, ANSS ComCat and the contributing seismic networks. USGS license guidance distinguishes federal and partner data. We do not assume that every ComCat partner record has the same rights. Raw records and event-level or daily derived tables stay outside the signed package. Our original code, text, figure and coarse statistical results can carry the SCI baseline terms. The separate [external data notice](files/EXTERNAL_DATA.md) gives attribution and identifies this boundary. No paper text or source figure is bundled.

## Method

[design.txt](files/design.txt) was saved before weekday counts. It is a local plan, not an external registration. Its final boundary rule is the full local-day rule above; earlier alternatives written in that file were not used.

Let x(d) = (cos(2 pi w/7), sin(2 pi w/7)), where w is zero for Monday through six for Sunday. For each training month, subtract the month's event total times the mean of x over its calendar days from the event-weighted sum of x. Add these adjusted vectors over training months to obtain v. The fixed training direction is u = v / length(v). Training amplitude is 2 length(v) / N_train. This amplitude is selected to be nonnegative and is not evidence of a pattern by itself.

In testing, compute the same month-adjusted vector V without fitting its direction. The score is A = 2 u dot V / N_test. A positive score means alignment with the training phase. A negative score means opposition along that direction. It is a relative first-harmonic projection, not a percent change in total earthquakes, a weekend rate ratio, or a fitted physical forcing amplitude. For a pure sinusoidal daily rate with balanced exposure it equals amplitude times the cosine of the phase gap. The calendar adjustment removes the contribution of month totals and weekday exposure.

For each test month, compute the score sum for every circular rotation of its daily count sequence. Draw one rotation independently per month in each of 19,999 replicates. Monthly totals remain fixed. The null assumes that the count sequence has no preferred calendar position within each month. It preserves most local clustering, but cuts groups at month limits and adds a wrap boundary. The exact mean of the adjusted null is zero. The two-sided p value is (1 + count of absolute null scores at least as large as the absolute observed score)/20,000. Seed is 45120 for primary, with increments by case. The Monte Carlo standard error near the primary p is about 0.0019.

For an interval, sample the 21 test years with replacement in 19,999 draws. Add their centered score sums and event totals, then form the ratio. This fixes the training phase and assumes independent, exchangeable years. It does not include phase uncertainty, catalog error, or long-range dependence. Checks use the other sites, Geysers M2.5+, local civil dates, and whole-year rotations. Each site or threshold gets its own early phase. The whole-year check uses annual rather than monthly centering for both its score and bootstrap. Checks have no multiple-test correction and do not support separate discoveries.

## Results

| Test | Training events | Test events | Projection, % | Conditional 95% interval, % | Shift p |
| --- | ---: | ---: | ---: | --- | ---: |
| Geysers M2+, primary | 5697 | 5441 | -3.87 | -8.33 to +0.79 | 0.07660 |
| Coso M2+ | 1918 | 1163 | -10.82 | -19.94 to +13.00 | 0.32325 |
| Salton Sea M2+ | 1394 | 1411 | -15.15 | -65.10 to +37.51 | 0.68485 |
| Geysers M2.5+ | 1685 | 1419 | -5.06 | -11.76 to +2.40 | 0.22145 |
| Geysers civil dates | 5697 | 5441 | -4.04 | -8.22 to +0.26 | 0.06250 |
| Geysers year shifts | 5697 | 5441 | -3.83 | -8.39 to +0.92 | 0.05985 |

The primary early amplitude was 2.32%. Its fixed phase had a negative later projection. Every specified interval includes zero. The small positive upper endpoint in the primary interval is conditional on one uncertain early phase; it is not a general bound on a physical weekly effect. Coso and Salton Sea have larger early amplitudes, but their test scores remain uncertain. The wide Salton Sea interval shows the small effective information content of clustered counts. We did not test whether the negative scores differ among sites or establish a common phase reversal.

## Validation and limits

The separate [audit.py](files/audit.py) uses scalar date arithmetic, Python calendar lists and direct circular indexing for the primary result. It matches all training and test weekday counts and exposure days, the fitted direction, test projection and exact rotation variance. It also checks the saved null tail and bootstrap quantiles. [audit.json](files/audit.json) records a pass. Analysis assertions check source hashes, unique event IDs, and simulation moments against exact rotation moments. These checks validate arithmetic, not the null assumptions.

This study cannot separate detection changes from physical rate changes. Weekly behavior can change after 2004, cancel across the field, use higher harmonics, or depend on magnitude. A weak early vector makes the learned phase uncertain. We test transfer of that vector, not all possible weekly patterns. No operation records, noise measurements, ETAS model, relocated catalog, reservoir geometry, or complete event-detection model were used. Month shifts do not preserve all clusters. Year resampling need not cover changes in catalog practice. These limitations prevent causal attribution and operational forecasting.

A useful next test would use daily injection and power records with a local stable-completeness catalog, keep a separate later test period, and model detection and triggered events. Changing phase and magnitude thresholds after seeing these results would need a new confirmation sample. The present test leaves that mechanism question open.

## Reproduce

Verify and extract the signed ZIP. Use Python 3.12 with numpy, pandas and matplotlib; versions are in environment.json. From the extracted publication root run, with new output paths outside it:

```sh
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --datasets /mnt/dell-data/shared_datasets --out /LOCAL/SCRATCH/repeat
python files/audit.py --source /mnt/dell-data/shared_datasets/comcat-geysers-m2p0-1984-20261110/comcat-geysers-m2p0-1984-20261110.csv --results /LOCAL/SCRATCH/repeat --out /LOCAL/SCRATCH/audit.json
```

Compare summary.json, weekday_totals.csv, the annual score tables and NPZ draws with the signed evidence. Plot bytes may depend on software versions. `python files/retrieve.py --scratch /LOCAL/SCRATCH/external` retrieves each recorded query separately and reports hash matches. This helper refuses an existing target directory and any target inside the publication. The helper makes the named dataset subdirectories with saved source metadata; pass its scratch root as --datasets. The saved metadata retain the original snapshot hash so that the analysis rejects changed source bytes. Revised live queries may have new bytes. Exact repetition then needs the preserved shared snapshots. The bundled coarse evidence remains inspectable without raw records. No private scratch is needed beyond these documented external inputs.

## Work record

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-65b6ca495a2d. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort, through the Codex harness in T3 Code. Date 12 November 2026 UTC. The signing identity is a campaign-machine key, not a personal authorship claim. No agents were launched. No private key is included. This worker saves a signed local publication only; it does not upload or submit it.
