# Public O4a and O4b gravitational-wave alerts compared with the GWTC-4.1 and GWTC-5.0 catalogs

## Summary

We compared all 3,558 public LIGO-Virgo-KAGRA (LVK) low-latency alerts (GraceDB superevents) in the
O4a and O4b catalog time windows with the final offline catalogs. GWTC-4.1 covers O4a and GWTC-5.0
covers O4b. The test asks whether the alert products predicted the catalog results. The products are
the astrophysical probability (p_astro), the source class, the distance and the sky map.

Main results:

1. **p_astro values below 0.9 were too high.** For the 2,500 compact-binary (CBC) alerts, the sum of the
   first-notice p_astro was 420.6. The sum of the catalog p_astro values for the same superevents was
   308.8, and 266 superevents went into the catalogs (offline p_astro >= 0.5). In the 0.1-0.5 bin
   (557 alerts, mean alert p_astro 0.22), the mean catalog p_astro was 0.11 and 7.2% went into the
   catalogs. In the 0.5-0.9 bin (93 alerts, mean 0.67), the mean catalog p_astro was 0.38 and 37% went
   into the catalogs (Figure 1).
2. **Most of the difference comes from one pipeline.** For alerts that the SPIIR pipeline issued first
   (455 alerts, mostly in O4a), the alert p_astro sum was 85.7. The catalog sum was 19.3, and 20 of these
   superevents went into the catalogs. For mid-range SPIIR alerts (0.1 <= p_astro < 0.9, n = 238),
   the mean alert p_astro was 0.24 and the mean catalog p_astro was 0.010. MBTA alerts also had high
   values (23.1 against 10.4). GstLAL (284.9 against 252.1) and PyCBC (24.5 against 19.2) had smaller
   differences, but these differences were also negative (Figure 2).
3. **A recalibration from O4a improves O4b forecasts.** We fitted a logistic recalibration with
   pipeline offsets on O4a alerts only and applied it to O4b alerts. The O4b Brier score for catalog
   membership went from 0.0344 to 0.0289 (paired bootstrap difference -0.0055, 95% CI -0.0091 to
   -0.0019). The log loss went from 0.142 to 0.118. A global recalibration without pipeline terms
   gave a smaller gain, and its interval included zero.
4. **The p_astro value did not identify the retracted alerts.** LVK retracted 20 public alerts (19 significant).
   None of them is in a catalog. Their first-notice p_astro was above 0.9 for 9 of them. For significant
   alerts that LVK did not retract, the last-notice p_astro sum (186.7) was near the catalogued
   count (181 of 191).
5. **The first BAYESTAR sky maps were slightly too narrow. The updated online-PE sky maps were
   more narrow.** We used the catalog parameter-estimation (PE) sky map as the reference posterior.
   The mean catalog-PE probability inside the alert 90% region was 0.858 (95% CI 0.840-0.875,
   n = 189) for the first BAYESTAR maps. For the last-notice online-PE (Bilby) maps it was
   0.828 (0.818-0.838, n = 165). For the 50% region, the values were 0.475 and 0.411. For the same
   164 events, the online-PE 90% regions were 26% smaller (median) than BAYESTAR. Their coverage was
   lower by 0.038 (95% CI 0.016-0.057) (Figure 3).
6. **First-notice distances had a tail of large under-estimates.** For 14 of 189 events (7.4%), the
   catalog distance was more than 3 alert standard deviations above the first BAYESTAR distance mean.
   An example is GW250119_025138: the alert gave 433 ± 113 Mpc and the catalog gave 3058 Mpc. All 14
   alerts came from the GstLAL pipeline first, and all are heavy binary black holes. Alerts first
   issued by other pipelines had no such errors (0 of 38; Fisher p = 0.077, a post-hoc test). The
   last-notice online-PE distances agreed with the catalog for all events (|z| < 1.645 for 165 of 165;
   Figure 4).
7. **Some catalog events had no public alert.** 30 of 301 catalog candidates (10%) had no public
   alert. Their median offline p_astro was 0.68. Five had p_astro >= 0.9. These include
   GW240414_054515 (offline FAR about 5e-5 per year, H1-V1) and GW240519_012815 (L1-V1).
   181 of 301 (60%) had a significant public alert.
8. **The source-class probabilities agreed with the catalog, but the test has low power.** Two
   catalog events with PE have m2 < 3 Msun (GW230518_125908 and GW230529_181500). Both had HasNS = 1.0
   in the first notice. For the 190 catalogued events with PE, the HasNS sum was 3.24, and the
   catalog has 2 neutron-star events. Four binary black holes had HasNS > 0.1.

## Question and why it is important

Astronomers use LVK public alerts to decide which gravitational-wave candidates to follow up with
telescopes. Each alert gives a probability that the source is astrophysical (p_astro), a source class,
and a three-dimensional sky map. If these numbers are not calibrated, follow-up programs use telescope
time on false alarms, or they search areas that are too small. The final catalogs for O4a (GWTC-4.1)
and O4b (GWTC-5.0, released 2026-05-26) now let us do an independent check of the alerts as LVK
issued them. We used only public data. Before this comparison, we wrote the plan in
`files/analysis_plan.md`.

## Data

| Input | Source | Version / hash |
|---|---|---|
| Public superevents (3,558; O4a window GPS 1368300000-1389460000, O4b window 1396400000-1422120000) | GraceDB REST API, `https://gracedb.ligo.org/api/superevents/` (unauthenticated = public only), retrieved 2026-11-09 | `files/data/inputs/gracedb_public_superevents_*.json.gz` |
| VOEvent notices (first and last non-retraction notice per superevent) | GraceDB `/superevents/<id>/voevents/` and files | parsed table `files/data/derived/alert_params.csv`; sha256 of every downloaded XML and sky map in `files/data/inputs/gracedb_downloaded_files_sha256.txt.gz` |
| Alert sky maps (542 files for the 271 catalogued superevents) | `skymap_fits` URL from each VOEvent | sha256 list as above (408 MB, not included) |
| GWTC-4.1 candidate search summary | Zenodo 10.5281/zenodo.20276095, `IGWN-GWTC4p1-18965dda8_5-SearchSummaryTable.hdf5` | md5 f2d06f3aab80de8ec4aa97664b323498, sha256 af99b484...ac0f (included) |
| GWTC-5.0 candidate search summary | Zenodo 10.5281/zenodo.20348004, `IGWN-GWTC5p0-29ebe06b7_25-SearchSummaryTable.hdf5` | md5 d4c0e5e32bb00139eaaaa15fb810d95b, sha256 419ce370...14f3 (included) |
| GWTC-4.1 PE sky maps | Zenodo 10.5281/zenodo.20275769, `IGWN-GWTC4p1-18965dda8_5-Archived_Skymaps.tar.gz`; shared campaign dataset `datasets/gwtc4p1_pe_archived_skymaps` | md5 28de7ccf80d08da3eb9fb374939d511a, sha256 8fbe990e...da7e8eb |
| GWTC-5.0 PE sky maps (Part 1; 104 O4b events) | Zenodo 10.5281/zenodo.20348005, `IGWN-GWTC5p0-29ebe06b7_25-Archived_Skymaps.tar.gz`; shared campaign dataset `datasets/gwtc5p0_pe_archived_skymaps` | md5 6a4b5d6fc3f62d350be9b73dae1796c8, sha256 175b3d92...faf4496d8c3f96eeeea2cd31eafbb77f0aafda7e |
| PE summary tables | Zenodo 20275769 and 20348005 (`*-PESummaryTable.hdf5`) | included |
| Catalog source-property medians | GWOSC `https://gwosc.org/eventapi/jsonfull/GWTC-4.1/` and `/GWTC-5.0/`, retrieved 2026-11-09 | sha256 c0ca235a... and 5a15bccb... (included, gzip) |

All Zenodo md5 values that we computed agree with the values that the Zenodo API gives.

## Method

* **Matching.** The catalog search summary tables give the GraceDB `superevent_id` for each offline
  candidate (1,456 in O4a and 1,886 in O4b, all with FAR < 2 per day in some pipeline). We matched
  public alerts by this ID. A superevent that is not in the table gets offline p_astro = 0. We did a
  time match (|dt| < 0.5 s) for unmatched alerts. It found 21 more offline candidates, and all of
  them have offline p_astro < 0.5.
* **Labels.** "Catalogued" means offline p_astro >= 0.5 (the catalog inclusion rule; 140 O4a and
  161 O4b candidates). We also use the offline p_astro as a soft label. If both the alert and
  the catalog probabilities are calibrated posteriors, and the catalog uses at least the same
  information, then E[offline p_astro | alert p_astro] = alert p_astro (tower property). Thus the soft-label
  test does not need ground truth. But it does need a calibrated catalog p_astro.
* **As-issued values.** We used the first non-retraction notice (normally the first Preliminary
  notice). For significant alerts we also used the last notice.
* **H1 statistics.** Reliability bins, Wilson intervals, bootstrap intervals for mean offline p_astro,
  count z-scores (observed - expected) / sqrt(sum p(1 - p)), Brier score and log loss. Out-of-sample
  recalibration: logistic model on logit(p_astro) with offsets for the first-alert pipeline, fitted on
  O4a and scored on O4b. Paired bootstrap for the Brier difference.
* **H4 sky coverage.** We converted both maps to HEALPix nside 512 (nested) with `ligo.skymap`. For
  each alert credible level X, we calculated the catalog-PE probability inside the alert X region.
  If the alert maps are calibrated relative to the catalog posterior, the event mean of this
  quantity equals X. This is the same tower-property argument as for p_astro. We used the "Mixed"
  catalog PE map (170 events). If it was not available, we used "IMRPhenomXPHM_SpinTaylor" (208 map
  pairs including both notices) or, for 2 map pairs, another waveform.
* **H3 distance.** z = (PE distance mean - alert DISTMEAN) / alert DISTSTD, with values from the
  FITS headers.
* Code: `files/code/01_...` to `07_...`; the run order is in `files/code/run_all.sh`.

## Results tables

H1, all 2,500 CBC alerts with p_astro (`files/results/h1_reliability_bins.csv`, subset "all"):

| alert p_astro bin | n | mean alert p_astro | mean catalog p_astro (95% CI) | fraction catalogued (95% CI) |
|---|---|---|---|---|
| 0-0.01 | 914 | 0.003 | 0.006 (0.004-0.008) | 0.001 (0.000-0.006) |
| 0.01-0.1 | 741 | 0.055 | 0.044 (0.035-0.053) | 0.020 (0.012-0.033) |
| 0.1-0.5 | 557 | 0.219 | 0.113 (0.097-0.130) | 0.072 (0.053-0.096) |
| 0.5-0.9 | 93 | 0.669 | 0.377 (0.304-0.452) | 0.366 (0.275-0.467) |
| 0.9-0.99 | 54 | 0.961 | 0.831 (0.740-0.912) | 0.870 (0.756-0.936) |
| 0.99-1 | 141 | 0.999 | 0.909 (0.861-0.952) | 0.915 (0.857-0.951) |

Totals by first-alert pipeline (`files/results/h1_summary.csv`):

| subset | n | sum alert p_astro | sum catalog p_astro | catalogued |
|---|---|---|---|---|
| all | 2500 | 420.6 | 308.8 | 266 |
| GstLAL | 878 | 284.9 | 252.1 | 220 |
| MBTA | 389 | 23.1 | 10.4 | 6 |
| PyCBC | 499 | 24.5 | 19.2 | 18 |
| SPIIR | 455 | 85.7 | 19.3 | 20 |
| SPIIR O4a / O4b | 384 / 71 | 75.5 / 10.2 | 13.3 / 6.0 | 14 / 6 |
| cWB (BBH search) | 279 | 2.4 | 7.8 | 2 |
| significant alerts | 197 | 189.8 | 170.1 | 172 |
| low-significance alerts | 2303 | 230.8 | 138.7 | 94 |

Sky coverage (`files/results/h4_coverage_table.csv`):

| alert maps | n | PE mass in alert 50% region | PE mass in alert 90% region | median area90 alert / PE |
|---|---|---|---|---|
| first notice, BAYESTAR | 189 | 0.475 (0.451-0.500) | 0.858 (0.840-0.875) | 1.15 |
| BAYESTAR, 2 detectors | 126 | 0.472 | 0.860 | 1.09 |
| BAYESTAR, 3 detectors | 52 | 0.504 | 0.855 | 1.35 |
| last notice, online PE | 165 | 0.411 (0.399-0.424) | 0.828 (0.818-0.838) | 0.85 |

## Interpretation

The alert p_astro values were too high where they matter most for follow-up decisions (0.1-0.9).
This was strongest for SPIIR-first alerts in O4a. The catalog has no SPIIR offline analysis. But a real
signal that SPIIR found should also be found by the offline GstLAL, PyCBC, MBTA or cWB analyses.
Thus a mean catalog p_astro of 0.010 for SPIIR alerts with a mean alert p_astro of 0.24 is not
consistent with a calibrated SPIIR p_astro. The O4b SPIIR alerts were fewer and closer to calibration.
This agrees with a change in SPIIR behaviour between the two parts of the run, but we did not
examine the pipeline configuration. Users can apply a simple pipeline-aware recalibration that
was fitted on earlier alerts, and it improved forecasts for the later run.

The sky maps were slightly too narrow relative to the catalog posteriors. This is consistent with
two causes: the low-latency analyses do not include detector calibration uncertainty, and the
catalog uses better waveform models. We did not separate these two causes. The online-PE update
made the regions about 26% smaller but did not keep the coverage. A follow-up program that uses
the updated 90% region gets about 83% of the catalog probability, not 90%. For first-notice distances,
the large under-estimates (factor 2-7) for some heavy binary black holes found by GstLAL are a
practical risk for galaxy-targeted follow-up. The cause is not known. A possible cause is a
template-mass or SNR-series mismatch in the trigger that went to BAYESTAR. The public alerts do not
contain the template masses, so we could not test this.

## Limitations

* The catalog p_astro is not ground truth. It depends on the population model and on the offline
  pipelines. The soft-label test assumes that the catalog p_astro is calibrated. If the catalog
  p_astro is too low, part of the difference comes from the catalog and not from the alerts.
  The hard-label test (catalog membership) uses a 0.5 threshold. For this reason, a calibrated
  alert p_astro near 0.5 is not expected to match the catalogued fraction exactly.
* The alerts and the catalog use the same strain data. Their errors are not independent. Sky-map
  "truth" is the catalog PE posterior, not the true source position.
* The sky and distance tests use only catalogued events with a released PE sky map (190 of 271).
  Twenty-one late O4b events (Part 2 of the GWTC-5.0 PE release) have their sky maps only inside
  large per-event HDF5 files, and catalog events with FAR > 1 per year have no PE. We did not use
  these events.
* Two catalog candidates (GW230904_152545 and GW231013_135504) have NS-class offline probabilities
  but no PE. The m2-based source-class test therefore uses only 2 neutron-star events and has very
  low power.
* We used the GraceDB files as they were on 2026-11-09. We used the first VOEvent of each superevent
  as the as-issued value. A small number of alerts had an early-warning notice first (7 superevents).
* We used the burst (cWB AllSky) alerts only for the counts. Of 1,058 burst alerts without p_astro,
  5 are in a catalog.
* The pipeline split uses the pipeline of the first notice. The preferred event can change later.
* The GstLAL distance-error result came from a test that we did not plan before we saw the data
  (p = 0.077). Treat it as a hypothesis.

## Reproduce

1. `bash files/code/run_all.sh` in an empty directory. This downloads the inputs (about 1 GB with
   sky maps), fetches about 7,000 GraceDB files (about 15 min with 8 threads), and runs steps 03-07.
2. Step 06 needs `ligo.skymap` (we used ligo.skymap 2.5.4, healpy 1.20.1, astropy 8.0.2,
   numpy 2.5.4, pandas 3.1.1 in a private uv environment, Python 3.12). Other steps used
   Python 3.12 with numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, matplotlib 3.11.2, h5py 3.16.0 and
   statsmodels 0.15.0.
3. On the campaign host, the PE sky-map tarballs are in `datasets/gwtc4p1_pe_archived_skymaps` and
   `datasets/gwtc5p0_pe_archived_skymaps`. You can extract them in place of the download.
4. To check a claim without the downloads, use `files/data/derived/merged_alerts.csv.gz` (one row
   per public superevent with alert and catalog values), `cbc_alerts_scored.csv.gz`,
   `catalog_events.csv`, and `files/results/*`.

## Files

* `files/analysis_plan.md`: the plan that we wrote before the comparison.
* `files/code/`: all scripts.
* `files/data/inputs/`: the small catalog tables, the GraceDB superevent lists, and the hash lists.
* `files/data/derived/`: merged tables.
* `files/results/`: summary tables and JSON (H1-H6).
* `files/figures/`: Figures 1-4.

## Provenance

* Job: sci-1107-dell-astronomy-008b4384d9bb; topic: astronomy; campaign 11_07_2026; machine: dell;
  account: claude-andrii; model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a
  campaign-machine key and is not a personal authorship claim.
* Data: LVK public alerts (GraceDB) and LVK catalog data releases (Zenodo, GWOSC). The analysis
  is independent and does not come from the LVK collaboration.
