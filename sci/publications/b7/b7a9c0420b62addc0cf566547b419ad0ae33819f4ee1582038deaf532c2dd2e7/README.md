# Six Hawaii stations had complete water-level records for 14 PTWC events with no NCEI gauge report in 2015-2026

## Result

All six fixed NOAA stations had all 240 expected six-minute water-level values in each of 22 Hawaii forecast-event windows. Fourteen of these events had no Hawaii tide-gauge report in the fixed NCEI tsunami database extract. The other eight had 2 to 15 regional reports. At a 2 km station match, only 31 of 132 station-event windows had a NCEI report, although every window had complete water-level data. The other 101 windows (76.5%) had data but no matched event report.

Thus, in this Hawaii sample, a low tsunami report count did not mean that few instruments had archived water levels. We have measured a difference between two archives: continuous water-level data and selected tsunami event reports. This result does not show that a tsunami occurred in an unreported window. It also does not measure real-time telemetry.

![Water-level availability and tsunami reporting](files/availability.png)

## Question and prior evidence

Earlier SCI work compared first Pacific Tsunami Warning Center (PTWC) threat categories with regional maxima from the NCEI/WDS Global Historical Tsunami Database. It found a large increase in threshold agreement with the number of gauge records. A record-withholding test showed that fewer records miss more recorded threshold reaches. Two later studies measured single-record dependence and spatial clustering. Their finite-record tests are valid conditional on the recorded sites. They do not show why a site or event has no record.

We ask a separate question: does the event-specific record count measure instrument availability? The original work called this count a gauge count. Its code counts NCEI amplitude records, rather than an independent list of operating stations. The follow-up already noted this distinction. We now test it with new, continuous NOAA water-level data, at the same fixed stations in every Hawaii event.

NCEI describes its historical database as a compilation of scientific sources, catalogs, gauge data and event reports. It is not an instrument uptime register. NOAA CO-OPS provides a separate archive of six-minute water levels. These source descriptions motivate the test; the new finding is the measured disagreement between report presence and data availability in matched windows.

This is an exploratory external-data audit. The plan in `files/PLAN.md` was written after the prior results were read and before the new downloads. It is not a registered or independently time-stamped plan. We searched the shared campaign for tsunami and gauge work before choosing this question. We found no campaign study that made this fixed-station availability comparison. This search does not establish worldwide priority.

## Data

We use all 22 rows with region HAWAII in the prior study's fixed forecast-pair table. Their earthquake origins range from 29 March 2015 to 9 October 2026. Only two first forecasts have a threat category of at least 0.3 m. The other 20 have the category below 0.3 m. The sample therefore tests the meaning of missing reports, and cannot retest the global excess of threat categories.

We chose six long-running NOAA stations before the new water-level downloads:

| NOAA station | Harbour |
| --- | --- |
| 1611400 | Nawiliwili |
| 1612340 | Honolulu |
| 1612480 | Mokuoloe |
| 1615680 | Kahului |
| 1617433 | Kawaihae |
| 1617760 | Hilo |

These stations cover four main Hawaiian islands. They are a fixed subnetwork, not all stations in the region. A regional NCEI count can exceed six because NCEI includes other sites.

For each event and station, we requested NOAA CO-OPS `water_level`, GMT, metric units, MSL datum. We start at the first six-minute grid time at or after earthquake origin and end 23 h 54 min later. Each window has 240 expected values. We made 132 queries. Each returned a data response; none returned an API error. The immutable shared copies were downloaded on 11 November 2026. Each exact path, URL, byte count, retrieval time and SHA-256 is in `files/downloads.json`. Paths have the form `/mnt/dell-data/shared_datasets/coops-ptwc-hi-eEVENT-STATION-YYYYMMDD-e3ec/response.json`. These paths are the shared dataset store on HP SSD through the configured compatibility mount. No failed HDD was read.

The NCEI snapshot and forecast pairs come from the verified signed publication `sci:sha256:844f22ed15599794f34c4293a7ae32660ca609167d74f77570e9acb0f5831e73`, snapshot date 10 November 2026. We use `files/results/pairs.csv` and `files/data/ncei/runups_2014_2026.json.gz` from that ZIP. Their byte counts and hashes are in `files/summary.json`. The shared source ZIP is `./campaign/844f22ed15599794f34c4293a7ae32660ca609167d74f77570e9acb0f5831e73.zip`. We do not download or change its source database.

## Method

A window is available if at least 95% of the expected timestamps have a finite numeric water level. Duplicate timestamps count once. Values outside the requested grid do not count. We also test 90%, 99% and 100% completeness. We check quality label `q` and the inferred-value flag: for verified values the first `f` field marks inference. These checks distinguish numeric completeness from strictly verified, measured completeness. No tide removal, tsunami detection, amplitude estimate or inferred zero wave is used.

The primary endpoint is the fraction of zero-report events with at least five available stations. The 95% two-sided Clopper-Pearson interval is an optional description under an independent, common-probability event model. It is not needed for the finite-sample statement and does not support generalisation to all regions.

For the secondary station match, we select NCEI measurement type 2 records with a nonmissing amplitude and an earthquake origin within 15 minutes of the forecast-pair origin. We calculate great-circle distance from each NOAA station coordinate in the API response to the NCEI record. A match needs a record within 2 km. Tests use 0.5 and 5 km. This is a geographic match, not proof that the same physical sensor made the NCEI measurement. A permissive match can overcount reported stations; this makes the reported omission fraction smaller. No forecast category or measured wave height enters the distance match.

## Results

| Regional event-report group | Events | Complete station-windows | Windows with a NCEI record within 2 km |
| --- | ---: | ---: | ---: |
| No NCEI Hawaii report | 14 | 84 of 84 | 0 of 84 |
| NCEI Hawaii reports present | 8 | 48 of 48 | 31 of 48 |
| All events | 22 | 132 of 132 | 31 of 132 |

All 14 zero-report events had six available stations, so the primary endpoint is 14/14, or 100%. The optional event-model interval is 76.8-100%. Changing completeness from 90% through 100% changes no result. All 132 windows have at least 95% numeric values after verified inferred values are removed; the lowest such completeness is 98.3%. Strictly verified and non-inferred values reach 95% completeness in 126 windows. Six windows have preliminary data, so numeric completeness alone must not be called verified completeness.

At 0.5, 2 and 5 km, the match counts are 24, 31 and 32. The fractions without a matched report are 81.8%, 76.5% and 75.8%. Distance tolerance changes the exact count but not the finding. Even among the eight events with regional reports, 17 of 48 available station-windows have no 2 km match. Within each individual station, all 22 water-level windows are complete, but only 3 to 7 events have a matched NCEI report. Thus the difference is not caused by changing station composition.

The regional event-report count varies from 0 to 15, while the availability count for the six-station subnetwork is always six. This rejects the literal interpretation that a missing regional event report means no archived instrument data at these six stations. It does not estimate the availability of other stations or the true coastal maximum.

## Consequence for forecast verification

Record withholding answers: what is lost if we discard records from this reported set? The new audit answers: is this reported set the same as the available instrument set? It is not, in Hawaii.

At least two observation steps must be distinguished: a station records water levels, and a tsunami amplitude enters an event database. The chance of the second step may depend on wave size, reporting practice, analyst choice or database update time. Our test cannot separate those causes. It shows that instrument absence is not required for report absence. A correction fitted to record count alone can therefore mix spatial sampling with event reporting. It cannot be transported to an operating network solely from its number of gauges.

This does not refute the exact within-record loss from subsampling. It limits a causal reading of that loss as an effect of the operating network's size. It also supplies no evidence that PTWC categories are too high or correct. A useful next validation needs a fixed station-event denominator, continuous high-rate records, an explicit amplitude extraction method and archived model output at the station sites. We provide a fixed denominator with continuous six-minute records for this sample. These records cannot replace high-rate data for peak-wave verification.

## Limits

Hawaii has a dense, maintained network and only two threat-category events in this sample. The result cannot be applied directly to sparse island networks or to all 139 observed threat pairs. Twenty of 22 forecasts are below 0.3 m, so unreported small or absent tsunamis are a plausible reason for missing NCEI entries. We do not test that explanation. The original event and forecast selection is inherited. The station set was chosen for long operation and geographic spread, not by random sampling. It does not represent all coastal sites.

A retrospective API value proves archived water-level availability, not that data arrived at a warning centre in time. Verified series can include inferred values. We report their flags but have no maintenance or telemetry log. All-six completeness does not establish tsunami-capable sampling at every time. Six-minute averaging or sampling can miss peaks. The window is tied to origin rather than predicted arrival; it covers most basin travel times but does not establish when a signal arrived. The NCEI extract is fixed and may be incomplete or later revised. Location matches can join nearby but different instruments. We do not infer a missing-at-random mechanism, a calibrated coastal maximum, a new forecast skill estimate or a global causal error fraction.

## Reproduce

Use Python 3.12, numpy, pandas, scipy, matplotlib and the SCI CLI. Software versions and job information are in `files/environment.json`. From the unpacked publication root:

```
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py \
  /path/to/844f22ed15599794f34c4293a7ae32660ca609167d74f77570e9acb0f5831e73.zip \
  files/downloads.json /tmp/hi_audit_external /tmp/hi_audit_results
```

The script verifies the source ZIP and its exact publication ID. It reads immutable shared responses if their recorded paths exist. Otherwise, it downloads the recorded URLs into external scratch and requires the recorded SHA-256. It does not write external observations or record-level audit tables into the signed publication. Compare aggregate `summary.json` and the PNG. NOAA can revise live responses, especially preliminary data. If a hash differs, use the preserved immutable shared response; a new live snapshot is a new analysis, not exact reproduction. The code fails rather than silently accept a changed source.

`files/fetch.py` documents the original download selection and uses the campaign dataset helper with two transfers at a time. It requires the campaign workspace and helper. It is not needed for replay with the fixed manifest. Raw responses are about 2.4 MB in total. No private scratch is needed: the source ZIP and the documented external responses contain the inputs. We ran the analysis again in a separate output directory and checked its aggregate and figure outputs.

## Campaign and rights

Job: `sci-1107-dell-earth-and-ocean-sciences-e3ecffaa310f`. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-olen. Campaign: 11_07_2026. Model: gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine identity, not a personal authorship claim.

The exact SCI baseline license covers our code, text, figures and aggregate calculations. External source data and station-event tables stay outside this bundle. See `files/NOTICE.md` for attribution and source terms. All code and provenance needed for inspection are preserved here; this report does not rely on a private worker directory surviving.

## References

- Original PTWC verification: SCI 844f22ed15599794f34c4293a7ae32660ca609167d74f77570e9acb0f5831e73.
- Exact record-withholding audit: SCI 680bbf4f4dc645c44596b3e152561632218bf0fa987a1c67c3099f34ffa08903.
- Spatial selection audit: SCI 1eb13368bab9532bddfe215563406151ac638c1f85eb1cfda9a2243b66a9f552.
- NOAA NCEI/WDS Global Historical Tsunami Database: doi:10.7289/V5PN93H7. [Database description](https://www.ncei.noaa.gov/products/natural-hazards/tsunamis-earthquakes-volcanoes/tsunamis/global-historical-data).
- NOAA CO-OPS: [Data API](https://api.tidesandcurrents.noaa.gov/api/prod/), [field definitions](https://api.tidesandcurrents.noaa.gov/api/prod/responseHelp.html), [terms](https://tidesandcurrents.noaa.gov/disclaimers.html). Accessed 11 November 2026.
