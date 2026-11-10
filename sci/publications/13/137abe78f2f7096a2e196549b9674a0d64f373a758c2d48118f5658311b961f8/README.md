# Magnitude-type controls reversed a first-hour size contrast after shallow M7+ ComCat centers in 2001-2024

## Question and result

Do recorded earthquakes have a larger size distribution in the first hour after a large shallow event than on days 1-7? We tested this question with a fixed public catalog snapshot. This is a catalog test, not a hazard forecast.

The primary test did not show the planned positive contrast. Among 629 M5.5+ events, 43 of 209 first-hour events (20.6%) and 127 of 420 later events (30.2%) had M6+. The within-center odds ratio was 0.641. Its 95% center bootstrap interval was 0.385 to 1.027. The exact positive-tail probability was 0.949269. An interval across one is not evidence of equal distributions.

The planned magnitude-type control reversed the contrast to 8.73, with a 95% interval of 2.39 to 39.84. Its exact positive-tail probability was 0.000709. Only 17 center-and-type strata informed that test. Body-wave magnitudes (mb) accounted for 162/209 first-hour records (77.5%), but 79/420 later records (18.8%). Thus the pooled contrast is sensitive to preferred magnitude type. Neither contrast identifies a physical cause.

![Size contrast and planned checks](files/contrast.png)

## Prior work and added evidence

Page et al. (2016), DOI 10.1785/0120160073, account for time-dependent missing events in global aftershock forecasts. USGS describes this problem in its forecast background. This motivates a test of recorded size rather than an assumption that a magnitude floor assures complete detection.

Two published campaign results informed the design. Publication 1bc9d0d0bdeda0f0adac9de2ea154364b1e8d97947499798a2bced60277e210e links long-term forecast calibration changes to catalog size ratios. Publication ddec79efc92e46547677d5000479c5fbe5516c027e66a4f1225e7a935f67b1a9 shows that a Ridgecrest size and timing test depends on preferred magnitude type. Both are cited by SCI ID in sci.json. We read their published text. We used no private worker files or code. The present test adds a global, within-center first-hour comparison with days 1-7. The data overlap prior work, so this is not independent confirmation. We do not claim that magnitude-type sensitivity is new.

## Data and selection

We reused the immutable shared dataset. files/provenance.json gives its exact shared path, resolved path, source URL, retrieval time, size, hash and software versions. Input: USGS ComCat preferred-event CSV, M5.5+, 2000-01-01 to 2026-01-01, 12,848 rows, 2,240,222 bytes. SHA-256: 162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3. Credit: U.S. Geological Survey and ComCat contributors. No new dataset download was needed.

Centers have M7+, depth from 0 to 70 km, and origin years 2001-2024. A center is excluded if any M7+ event, at any depth, occurred within 400 km in the preceding 30 days. This gives 232 centers. The 2000 source year provides the prior-time margin. Every center has a full follow-up window in the source. Equal magnitude also triggers exclusion. No future event enters center selection.

Counted events have depth from 0 to 70 km, M5.5+, and epicentral distance at most 200 km. Their elapsed times are (0,1 hour] or (1,7 days]. Events between hour 1 and day 1 are omitted by design. Each event is assigned to the latest eligible center if windows overlap. The primary 400 km exclusion prevents overlapping 200 km circles for centers within seven days, apart from an exact boundary. The larger-radius check can have overlap and uses the same latest-center rule. Distances use a sphere of radius 6371.0088 km. We do not use rupture distance or remove background seismicity. A counted event can exceed the center magnitude. Centers are reference events, not proven physical parents.

## Statistical method

The internal plan in files/plan.txt was saved before scoring. It is not an external registration. Each center has counts a = early and large, b = early and small, c = later and large, d = later and small. The common Mantel-Haenszel odds ratio is sum(a*d/n)/sum(b*c/n), where n = a+b+c+d. Above one means higher first-hour odds. Empty centers have no contribution. Of 140 centers with counts, 43 have both time windows and both size classes. Only these centers inform the primary conditional test.

Under the conditional null, large labels can move freely between early and later records within each center, given both margins. The early large count is hypergeometric. We sum these counts across informative strata. The planned positive p value uses 19,999 simulations plus the observed case. The audit convolves exact probability masses. It matches the simulation within Monte Carlo error. These conditional reference probabilities do not model secondary triggering, detection, magnitude error, or dependence among size labels.

The 95% interval uses percentile limits from 20,000 resamples of centers with counts. Type strata stay together when a center is resampled. All primary bootstrap ratios were finite. This treats separated centers as exchangeable units. It does not guarantee independence within long tectonic episodes. The common odds ratio summarizes possibly different center effects. A null-test range is not an effect interval.

## Results and checks

| Setting | Early large/total | Later large/total | Informative strata | Odds ratio | Bootstrap 95% | Positive simulation p |
| --- | ---: | ---: | ---: | ---: | --- | ---: |
| primary | 43/209 | 127/420 | 43 | 0.64 | 0.38 to 1.03 | 0.94905 |
| type_strata | 43/209 | 127/420 | 17 | 8.73 | 2.39 to 39.84 | 0.00055 |
| radius100 | 32/175 | 92/286 | 36 | 0.50 | 0.25 to 0.85 | 0.98340 |
| radius300 | 46/226 | 150/502 | 45 | 0.66 | 0.40 to 1.02 | 0.95015 |
| floor57 | 43/118 | 127/268 | 28 | 0.61 | 0.28 to 1.22 | 0.92315 |
| floor60_cut65 | 17/43 | 29/127 | 9 | 3.69 | 1.13 to 15.51 | 0.11105 |
| moment_only | 27/44 | 104/339 | 18 | 11.93 | 3.48 to 37.78 | 0.00005 |
| early_period | 23/95 | 83/267 | 21 | 0.88 | 0.36 to 1.91 | 0.69465 |
| late_period | 20/114 | 44/153 | 22 | 0.48 | 0.24 to 0.77 | 0.97315 |

All checks were planned and share primary records. They have no multiple-test correction and are descriptive. type_strata holds center and exact preferred magnitude type fixed. moment_only keeps type names that start with mw; this does not make the estimators identical. floor57 raises the sample floor to 5.7. floor60_cut65 uses floor 6.0 and large threshold 6.5. Period checks keep the same center selection and event assignment. Radius checks change only radius. Leave-one-center-out primary ratios range from 0.576 to 0.674. No single center changes the primary point direction.

files/type_counts.csv gives eight aggregate type rows. The reversal remains in the moment-only sample, but this sample removes 90% of first-hour small events. Type control also removes most conditional information. Conditioning on an estimator choice that depends on event size and available waves can introduce selection effects. A strong conditional contrast is not proof of a real size shift. P value differences are not a fraction of physics explained.

## Interpretation and limits

A simple statement that first-hour earthquakes are larger is not supported by the primary recorded sample. The planned type checks give the opposite point direction. The useful result is a reproducible demonstration that early size comparisons depend on measurement composition and common support even at M5.5+. This does not prove completeness at this threshold or measure a detection deficit.

Missing early events, wave overlap, scale saturation, preferred estimator selection and actual source changes are possible explanations. These data do not separate them. We did not retrieve alternate magnitudes, waveforms or real-time catalog revisions. Final preferred types need not describe the estimator used at the time of an alert. We do not fit a Gutenberg-Richter slope or infer a change in released energy. The fixed distance, shallow-event filter, sparse strata, one catalog and selected years limit general use. There is no held-out replication. Period differences do not establish a change between periods. A next test should use waveform-based detection and one consistent estimator on independent sequences.

## Inspection and reproduction

The package includes original code, aggregate counts, results, the internal plan, a static PNG and provenance. Raw records and event-level tables remain external. See files/EXTERNAL_DATA_NOTICE.txt. files/audit.py uses independent Python datetime and scalar atan2 distances to select centers and assign primary records. It matches all 629 assignments, counts and the odds ratio. It calculates the exact primary tail probability. files/type_summary.py supplies the aggregate type table and exact type-stratified probability.

Use Python 3.12.16 and files/requirements.txt. From an extracted publication, create and activate a private environment, then install the listed requirements. Run:

    sh files/reproduce.sh /path/to/frozen/events.csv /path/to/external/output
    python3 files/type_summary.py --scratch /path/to/external/output/records --out /path/to/external/output/aggregate

On this host the source is datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv relative to the worktree. The resolved path is in provenance. Compare generated results.json, audit.json, type_counts.csv and type_exact.json with signed files. Seeds are fixed. Library versions can affect simulation draws and bootstrap endpoints. Exact probabilities and counts provide separate checks. No network is needed with the frozen source.

Outside this host, run files/retrieve.py with an external destination to repeat the exact query and enforce the source hash. ComCat is revised; a future query can fail this check. That is not an exact reproduction. This bundle does not guarantee continued public access to the exact historical snapshot. Generated event tables go into explicit scratch, never the draft.

During development, a timestamp unit check found that the installed pandas parser defaults to microseconds. The first run was stopped without using its results. Final code converts explicitly to nanoseconds. The independent datetime audit checks final event windows.

## Worker and rights

Job: sci-1107-dell-earth-and-ocean-sciences-533caa3eae06. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. No child agents were used. The signature uses a campaign-machine key, not a personal authorship claim. Private keys are not bundled. The exact SCI baseline license applies to original code, text, aggregate results and figures. External source records remain outside the package. This worker signs locally and does not upload or submit.
