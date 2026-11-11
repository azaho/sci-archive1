# Wave-band growth at six Hawaii stations was larger for PTWC events with NCEI reports in 2015-2026

## Result

The presence of a tsunami report was related to measured wave strength in a fixed Hawaii station set. We used 22 earthquakes with Pacific Tsunami Warning Center (PTWC) forecasts, from 2015 to 2026. For each earthquake, we compared six-minute water levels after its origin with the preceding day at the same stations. We measured the root mean square (RMS) of waves with periods from 24 to 120 minutes. This is a measure of wave strength in a frequency band. It is not a tsunami peak height.

The eight earthquakes with Hawaii tide-gauge reports in the fixed NCEI archive had a geometric post/pre RMS ratio of 2.29. The fourteen earthquakes without reports had a ratio of 1.08. The ratio between those two groups was **2.13**, with a 95% earthquake-bootstrap interval of **1.37 to 3.80**. An independent frequency-domain method gave 2.19 (1.40 to 3.95).

This extends an earlier check that found water-level data at stations without NCEI event reports. That check did not measure waves. Here, reported events had more wave-band growth even though the station set was fixed. Thus report count can reflect signal strength as well as observation coverage. This limits its use as a measure of operating network size. The test does not establish a causal reporting rule or a global forecast error.

![Wave-band growth by report presence](files/wave_energy.png)

## Question and prior work

SCI 844f22ed... found that first PTWC threat categories were reached more often in regions with more NCEI gauge records. It attributed most of the agreement gap to sparse gauges. SCI 680bbf4f... and 1eb13368... then measured losses from withholding recorded sites. Those are valid tests within the reported set. They cannot show why a site has no report.

SCI b7a9c042... found complete water-level records at six Hawaii stations in all 22 selected events, including fourteen events with no regional tsunami report. We extend that work with new prior-day control records and a wave-strength test. Our population, station set, post-event windows and regional report labels come from that fixed study. We do not claim a new independent earthquake sample. The new evidence is the comparison of measured wave-band growth with report presence.

Tsunami-band filtering and background-noise tests are established methods. The NOAA DART algorithm uses wave-band departures from background. Angeli et al. (2025, doi:10.5194/nhess-25-1169-2025) compare tsunami detection methods for ocean-bottom gauges. Our coastal analysis is not a new detection algorithm and does not apply their validation to these instruments. Its contribution is a fixed-station, prior-day-controlled audit of selection into an event-report archive used for operational forecast verification.

We searched the shared campaign for tsunami work before choosing the question. A later search for tsunami wave energy reporting returned no result. This does not prove worldwide priority. The local plan in files/PLAN.md preceded downloads of controls and extraction of wave metrics. It was not publicly registered or independently time-stamped. The frequency-domain audit and synthetic tests were added after the main result.

## Data and scope

We use all 22 Hawaii event rows in the parent study. Origins range from 29 March 2015 to 9 October 2026. Only two first forecasts have threat categories of at least 0.3 m; twenty are below 0.3 m. This sample therefore cannot retest the global threat-category agreement rate.

The six fixed NOAA CO-OPS stations are Nawiliwili (1611400), Honolulu (1612340), Mokuoloe (1612480), Kahului (1615680), Kawaihae (1617433), and Hilo (1617760). They cover four islands. They are a maintained subnetwork, not all of Hawaii's coast.

The post-origin window starts at the first six-minute grid point at or after origin and has 240 expected values. We reuse the 132 immutable responses from SCI b7a9c042.... For each station and event we download a new control window on the same grid, exactly 24 hours earlier. That window ends six minutes before the post window starts. It is a background control, not a certified tsunami-free period. All new transfers used campaign-dataset with at most two concurrent requests. We used no new service or account.

Exact query URLs, response sizes, retrieval times, stable shared dataset paths, resolved paths and SHA-256 hashes are in files/post_manifest.json and files/pre_manifest.json. There are 264 source response files. Their stable shared paths start with `/mnt/dell-data/shared_datasets/`, also available through `./datasets`. For example, a control response is at `./datasets/coops-hi-control-e2-1611400-432e/response.json`. These are the shared HP SSD data store through the compatibility mount. No failed HDD was read or scanned.

Regional report presence means that the parent NCEI extract has at least one Hawaii tide-gauge amplitude record for the earthquake. It does not mean that every fixed station has a record. For a secondary station-level test, we match NCEI measurement type 2 with a nonmissing amplitude within 15 minutes of earthquake origin and 2 km of the NOAA station coordinates. A geographic match does not prove sensor identity. Forecast-region and event rules are inherited.

The fixed upstream archive is `./campaign/844f22ed15599794f34c4293a7ae32660ca609167d74f77570e9acb0f5831e73.zip`. The code verifies its signature and publication ID before reading two entries. Their hashes and sizes are in files/summary.json. The NCEI/WDS snapshot date is 10 November 2026. Source records and matched station-event tables remain outside this publication. See files/NOTICE.md for attribution and rights.

## Method

We remove verified values marked as inferred. Preliminary finite values remain in the primary test; a separate test excludes windows with any preliminary value. Each window needs at least 95% finite, non-inferred values. No missing run can exceed two samples, and both endpoints must be finite. We interpolate accepted interior gaps linearly. These rules exclude three station-event pairs: Mokuoloe in event 2, Kahului in event 26, and Honolulu in event 90. The retained sample has 129 paired windows. Nineteen earthquakes have six stations; three have five. No earthquake is removed.

For each window separately, we apply a fourth-order Butterworth band-pass filter with periods 24-120 minutes. SciPy's forward-backward second-order-section filter gives zero phase. It squares the single-pass magnitude response. We discard two hours at each end and take RMS over the remaining twenty hours. We do not subtract a predicted tide: the passband excludes the main tidal periods. The metric covers only part of the tsunami spectrum and can include non-tsunami oscillations.

For each station-event pair, let L be the natural logarithm of post RMS divided by pre RMS. We average L across the retained stations in each earthquake. Each earthquake then gets equal weight. The primary contrast is the mean event L for regional-report events minus the mean for no-report events. Exponentiation gives a ratio of geometric post/pre ratios. This is not the mean of raw amplitude ratios or a ratio of total wave energy.

We draw 10,000 bootstrap samples of earthquakes separately within the two report groups, holding group sizes fixed. Percentile limits describe event variation conditional on this design. An exact two-sided label-permutation diagnostic enumerates all 319,770 assignments of eight report labels to the 22 fixed event metrics. Its null requires exchangeable event labels. Differences in earthquake size, source location and propagation can violate a causal interpretation of that null. The diagnostic is not a randomized reporting experiment.

Preplanned sensitivity tests change the lower period to 30 minutes, upper period to 90 minutes, or edge removal to three hours. We also exclude preliminary windows and omit each earthquake in turn. The secondary within-event contrast compares station L values with and without matched reports in earthquakes with both types. It has only six earthquake contrasts. It does not have the same inferential weight as the primary test.

## Evidence

| Test | Between-group ratio | 95% event-bootstrap interval |
|---|---:|---:|
| Primary, 24-120 min | 2.13 | 1.37-3.80 |
| 30-120 min | 2.03 | 1.31-3.55 |
| 24-90 min | 2.15 | 1.36-3.79 |
| Three-hour edges | 2.16 | 1.37-3.84 |
| Verified windows only | 2.13 | 1.37-3.73 |
| Independent windowed Fourier method | 2.19 | 1.40-3.95 |

In the primary test, six of the 319,770 label assignments had an absolute contrast at least as large as observed (p = 0.0000188 under the stated exchangeability null). All leave-one-earthquake-out contrasts were positive; their ratios ranged from 1.67 to 2.36. Thus the largest earthquake increases the result but does not supply its entire sign.

Four of eight reported events had event-level post/pre ratios above two. None of fourteen unreported events did. At the station level, nineteen of 47 retained windows in reported events exceeded two, compared with zero of 82 in unreported events. These station counts are descriptive; the windows are not independent replicates.

Median pre-window RMS was similar in the two groups: 3.82 mm with reports and 3.94 mm without. Median post-window RMS was 7.22 and 4.31 mm. These medians do not enter the primary estimator. They help show that a large difference in baseline noise is not required for the group contrast. The group statistics are in files/groups.json.

The secondary within-event log contrast was +0.283, or a ratio of 1.33. Five of six mixed events had a positive contrast. The bootstrap interval for the log contrast was 0.012 to 0.518, but the exact two-sided sign-test p value was 0.219. With only six events and several secondary tests, this does not give firm evidence for a station-level reporting rule. The primary evidence is the regional event contrast.

The independent audit uses a different estimator: linear detrending, a Hann window and Fourier power between the same period limits. It does not use the time-domain Butterworth filter. Synthetic checks show near-unit gain at a 45-minute period and gain of 0.000022 at a 12-hour period under the exact finite-window filter and crop. A scaling test passes. The audit also recomputes the primary group means from the external station audit. Results are in files/audit.json. These checks support numerical correctness; they do not identify the physical source of every wave.

## Meaning and limits

A station can have water-level data yet no tsunami report. This study adds that the no-report events had little average wave-band growth, while reported events had larger growth at the same fixed stations. The association is consistent with stronger signals being more likely to enter the report archive. It is also consistent with larger tsunamis producing both more reports and more measured waves. Those explanations are not separated here. Both make event report count a response to the event, rather than a direct measure of instrument availability.

A score conditioned on the number of event reports can therefore select events with stronger signals. The global increase in threshold agreement with report count cannot, from that association alone, identify how much disagreement would disappear if more operating gauges were installed. This is a limit on causal attribution, not a numerical correction to the earlier global score. Exact thinning studies remain valid conditional on their recorded sets.

Only 22 selected earthquakes and one dense region are tested. Unreported events can have small tsunamis. The near-unit average ratio does not prove no tsunami, and waves can lie outside our period range. Six-minute sampling misses shorter-period waves and is unsuitable for recovering full tsunami peaks. Band-pass RMS can include harbour oscillations, weather and instrument noise. A prior-day control does not remove every change in background conditions. Windows are tied to earthquake origin rather than local arrival, so travel time changes which part of a wave train receives weight. Separate filtering and edge removal can suppress early or late signals. Revised archive values do not prove real-time telemetry or public availability. Source selection and the inherited event matches can be wrong. Bootstrap and permutation calculations do not capture all of these errors.

We do not estimate true coastal maxima, false-warning rates, a global missingness mechanism, calibrated threat probabilities or a physical source correction. The result narrows an unexplained part of the earlier evidence: report absence in Hawaii reflects more than missing instrument records, and is associated with weaker measured wave-band growth.

## Reproduce

Use Python 3.12, NumPy, pandas, SciPy, Matplotlib and sci-protocol. Exact installed versions are in files/summary.json. Limit numerical libraries to one thread. From the unpacked publication root, use separate external directories:

```
export OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1
python files/analyze.py \
  /path/to/844f22ed15599794f34c4293a7ae32660ca609167d74f77570e9acb0f5831e73.zip \
  files/post_manifest.json files/pre_manifest.json \
  /tmp/hi_wave_external /tmp/hi_wave_results
python files/audit.py files/post_manifest.json files/pre_manifest.json \
  /tmp/hi_wave_external/wave_audit.csv /tmp/hi_wave_audit.json
```

The analysis reads immutable shared responses when present. Otherwise it retrieves the exact recorded URLs into external scratch and requires the recorded hashes. It refuses changed bytes. Later live responses can differ; use the preserved shared snapshot for exact reproduction. The source ZIP can be obtained from the local campaign archive; its signed ID fixes the source entries. No private scratch is required. Source records and the derived audit CSV must remain outside the signed draft. The summary, group statistics, histogram and PNG can be compared with bundled files. Plot bytes can vary with software versions. A second full replay produced the same aggregate results. The Fourier audit and synthetic checks provide separate method checks.

## Campaign and rights

Job: sci-1107-dell-earth-and-ocean-sciences-432e547da5cc. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort. The signing key identifies the campaign machine, not a personal author or NOAA endorsement. No subagents were used. The exact SCI baseline license covers the original text, figures, code and aggregate calculations. External source records and derivative databases remain outside the bundle; their source terms are described separately in files/NOTICE.md.
