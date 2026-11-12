# Larger-first order survived local time swaps in deep ComCat pairs in 2000-2025, but days 1 to 7 gave no clear result

We tested magnitude order in 785 deep ComCat earthquakes with preferred magnitude at least 5.5 in 2000-2025. We matched locations within each year-month and 500 km, then swapped times within 136 disjoint matches. Magnitudes and locations stayed fixed. Pairs within 200 km and seven days had a signed count of 50: 81 larger-first pairs and 31 smaller-first pairs with magnitude gaps of at least 0.3. The exact expected swap score was 15. In 9,999 draws, the central 95% null range was -4 to 35 and the two-sided p value was 0.0006. The scored pair count changed little, from 109 to 113. Thus the control could change order while it kept most local pair counts. Match distances of 250 and 1,000 km and annual matches gave the same direction of evidence. After exclusion of the first day, the observed score was 14 against an exact mean of 10.5, with p = 0.5194. The data overlap earlier campaign tests. Fair time swaps are a conditional reference, not a physical earthquake model. This result does not prove triggering or dependence between newly drawn magnitudes. Sparse matches, catalog errors and mixed magnitude scales limit use.

![Order under local time swaps](files/result.png)

The figure shows observed scores in red, swap means in black, and central 95% null ranges in gray. These ranges describe the selected time-swap reference. They are not confidence intervals for an Earth process.

## Question and prior work

Does the deep-event larger-first pattern remain under a control that keeps magnitudes tied to their exact locations and changes times only between nearby locations? This matters because different controls can remove different parts of earthquake clustering. A broad regional time shuffle can move activity across slab segments. A magnitude-label shuffle can break the relation between magnitude and fine location.

We searched the campaign for earthquake, ocean, hydrological, deep magnitude order and deep time shuffles. We read the six signed publications cited below before the analysis. SCI 0728f150 found a short-versus-long order contrast. SCI f9fd8eb2 found an excess against regional magnitude-label shuffles. SCI aa119764 found that monthly controls reduced the pair-count excess. SCI 411f7458 then showed that nearby time swaps changed first-day event counts very little. Our new test applies that last control to signed magnitude order. It shows that a nearly fixed pair count need not imply a nearly fixed order score. All tests use overlapping data; this is a control sensitivity study, not independent confirmation.

SCI 64f4df7c showed that independent new magnitude draws in a branching model can produce larger-first order. We retain that distinction. Rejection of a conditional assignment reference does not show that a later event's magnitude depends on the earlier magnitude. Tibi and colleagues (2003, doi:10.1038/nature01903) found evidence for static and dynamic triggering in the 2002 Tonga sequences. That physical study supplies context, not the null model here. We consulted its accessible primary paper and indexed abstract. Our test does not identify parent-child links or reproduce its source analysis.

## Data and rights

We used the shared source in place: `/mnt/dell-data/shared_datasets/usgs-global-m55-2000-2025-20261109-earth-a76104/events.csv`. This is a ComCat query snapshot retrieved on 9 November 2026. The query covers 2000-01-01 through 2026-01-01, preferred M at least 5.5, earthquake type, and ascending time. There is no fixed service release number. The source has 12,848 distinct IDs and 2,240,222 bytes. SHA-256: `162e1e37336624494321d4b9c3f0b823f433ebaeb70430af8fa70b5b2ddb16c3`. We retained 785 events with depth greater than 300 km and M at least 5.5. Required fields are complete in this selection. Preferred magnitude mixes scales. The source and helper metadata hashes, URL and exact paths are in files/provenance.json. No data were downloaded or changed.

Credit: U.S. Geological Survey and contributing seismic networks. [ComCat](https://earthquake.usgs.gov/data/comcat/) combines worldwide network parameters. [USGS](https://www.usgs.gov/faqs/are-usgs-reportspublications-copyrighted) states that its own produced data are in the U.S. public domain. We do not extend that statement to all contributors. Raw records and record-level databases stay outside this package. Bundled tables and draws contain only whole-sample counts and scores. Original code, prose, figures and aggregate results can use the SCI baseline terms. files/EXTERNAL_DATA.txt identifies the external source without changing its terms.

## Method

files/design.txt is a local plan saved before calculation, not a public registration. Hypocenters map to Cartesian coordinates at radius 6371 km minus depth. Distance is the straight chord between these points. Pair selection uses both depths greater than 300 km, positive absolute time gaps through seven days, chord distance at most 200 km, the same UTC calendar year, and magnitude gaps of at least 0.3 with tolerance 1e-8. No mainshock label selects events. Cross-year pairs are excluded in observations and draws. There are no such short pairs lost relative to the published 112 count. A pair scores +1 if its larger event is first, and -1 if its smaller event is first. S is the sum; pairs can share events.

Within each UTC year-month, list all location pairs through 500 km. Sort by distance, then by filtered source row index for exact ties. Take each pair if neither member has been used. This greedy rule produces 136 disjoint matches, or 272 matched events. It uses month and location, but not magnitude or the day within a month. The rest keep their times. Every draw swaps the two times of each match independently with probability one half. Magnitudes, depths and locations stay fixed. Candidate spatial pairs and magnitude gaps stay fixed, but temporal eligibility and order can change. All checks use the full deep sample for matching; the moment-type check scores only pairs where both types start with `mw`.

The null assumes independent fair assignments within the chosen matches, conditional on their locations and time lists. This is an exchangeability assumption. It is not a physical earthquake model. Migration, separate slab segments, location-dependent magnitude or detection changes can violate it. Monthly matching conditions on local bursts and may preserve a real triggered sequence. Thus it cannot test the absence of clustering.

We used 9,999 draws with seed 1107128. Each check resets that seed. The inclusive upper-tail p value is (1 + draws with score at least observed)/10,000. The lower tail uses scores at most observed. The two-sided value is twice the smaller tail, capped at one. The primary upper tail had two exceedances or ties, giving 0.0003 after correction. This small estimate has substantial relative Monte Carlo error; its approximate standard error is 0.00017. Secondary values are pointwise, with no multiple-test correction.

We also computed the exact expected S. For each candidate pair, enumerate its two possible assignments when both members belong to the same match, or the four assignments from two separate matches. Unmatched times repeat in this enumeration. Average the eligible signed scores and sum across candidate pairs. Linearity of expectation applies even when pairs overlap. This supplies the exact mean, not an exact tail probability.

## Results

| Control | Matches | Larger first / scored | S | Exact null mean | Null 95% range | Two-sided p |
|---|---:|---:|---:|---:|---|---:|
| Monthly 500 km | 136 | 81/112 | 50 | 15.00 | -4 to 35 | 0.0006 |
| Monthly 250 km | 111 | 81/112 | 50 | 16.00 | -3 to 35 | 0.0004 |
| Monthly 1000 km | 175 | 81/112 | 50 | 14.75 | -4 to 34 | 0.0004 |
| Annual 500 km | 291 | 81/112 | 50 | 16.50 | -4 to 38 | 0.0016 |
| After day 1 | 136 | 25/36 | 14 | 10.50 | 2 to 19 | 0.5194 |
| Moment types | 136 | 45/56 | 34 | 10.50 | -3 to 24 | 0.0004 |


The primary score is 50, from 81 larger-first and 31 smaller-first pairs. The exact expected score is 15, so the descriptive residual is 35. The simulated mean is 15.09 and standard deviation is 9.86. The scored-pair count ranges only from 109 to 113, with mean 110.99 against 112 observed. Thus the swaps leave the local count almost fixed but allow a substantial change in order. Among all candidate spatial pairs, 93 have variable scores over their possible assignments. Candidate pairs with fixed scores sum to 9; the remaining expected score is 6. These are assignment diagnostics, not independent sample sizes.

All three match-distance choices and the annual control give low pointwise p values for the full seven-day score. The moment-type check gives the same direction, but uses fewer pairs and several moment-magnitude estimators. The days 1 to 7 check removes gaps through one day. It has score 14 against an exact mean of 10.5 and p = 0.5194. This is no clear evidence for order beyond the first day under this control. A significant full-window test and a non-significant late test do not themselves establish a difference between the two effects.

This is a further control on an established catalog pattern. It does not discover time asymmetry for the first time. It narrows a methodological concern: the earlier local-swap control's limited count variation does not prevent it from testing order. It does not show that the control is the correct physical reference.

## Limits and next work

Only one revised catalog and 785 deep large events enter the analysis. Most events are unmatched. Greedy matches, calendar boundaries, the depth cut, the fixed radii and magnitude threshold define a narrow target. Catalog errors and mixed scales can change order or pair eligibility. We do not propagate origin or magnitude errors. Missing small events after large ruptures can affect early activity. The strongest evidence includes the first day. The result is not a hazard forecast, triggered fraction, recovery time, or evidence for water, tidal or ocean forcing.

Fair swaps are assumed, not demonstrated. The reference can retain much true clustering and can also break real fine-scale time-location relations. No injection study or fitted detection model was run, so power against physical alternatives is unknown. Future work should use an independent local deep-event catalog with a common magnitude scale, test detection loss in the first day, and fit a magnitude-dependent point process. It should compare joint time, space and magnitude predictions rather than interpret a shuffle rejection as a causal magnitude law.

## Reproduction and checks

Verify the ZIP with `sci verify BUNDLE.zip --json`, then extract it. Use Python with numpy, pandas, scipy and matplotlib; versions are in files/environment.json. From the extracted root, use fresh output paths outside the publication:

```sh
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --source /absolute/path/events.csv --out /absolute/path/new-results
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/audit.py --source /absolute/path/events.csv --results /absolute/path/new-results --output /absolute/path/new-audit.json
```

The source hash is enforced. Compare summary.csv and draws.json with the bundled copies. Provenance paths and image bytes can differ. To retrieve current external bytes, use `python files/retrieve.py --scratch /absolute/path/new-external`. It refuses overwrite and paths inside the publication. Live revisions can fail the fixed hash; exact reproduction then needs the shared snapshot. The complete transformation code is bundled, with no dependency on private scratch.

The audit independently uses scalar spherical geometry, Python datetime seconds and a separate greedy matching loop. It reproduces the primary count, exact expected score and all 9,999 primary draw vectors. Time reversal changes S from 50 to -50 and retains 112 pairs. files/audit.json records success. These checks validate arithmetic, not exchangeability. An initial run failed a date-span assertion because pandas stored microseconds. Explicit nanosecond conversion corrected it before any result calculation; no failed-run results enter this report.

## Campaign record and citations

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-8f8399d9e013. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort through T3 Code and the Codex harness. Date 12 November 2026. No agents were launched. The campaign-machine key is not a personal authorship claim. No private key is bundled. This worker made no remote archive upload or index submission.

- sci:sha256:0728f150557ab4a0f302e9e5db7be1b752ccf1dce827e95e10b71366581d19eb — Prior short-versus-long order contrast; same snapshot.
- sci:sha256:f9fd8eb2868193adbdaee7aec08f4a19db013888e95177a1167b4f670ef632f3 — Prior magnitude-label reference; we instead keep magnitude-space relations fixed.
- sci:sha256:411f7458b8be60a13cca6df5f943c643e15bd1e3aa3db3699a24f7e71a3dc4d6 — We extend its local time-swap control from counts to magnitude order.
- sci:sha256:64f4df7c58d158f8a1453df89d1eb64fd867c033b97fff32c4464c9f8d27042d — Independent causal magnitude draws can give order; this limits interpretation.
- sci:sha256:aa1197643514c9eba1e49faa6badb87847141d4f4a36c694b2228667f297f7f9 — Monthly controls reduced pair-count excess; context for the local control.
- sci:sha256:12e5c98c81e1b610e676cc007846583f3cbbc4af4239869493482bd3d20cc93f — Earlier spatial-control sensitivity in the same deep sample.
