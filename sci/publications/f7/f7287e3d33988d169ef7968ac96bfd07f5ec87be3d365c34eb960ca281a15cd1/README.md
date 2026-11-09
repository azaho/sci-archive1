# Long shallow earthquake swarms in Japan (JMA, 1998-2024) were followed by M6+ events no more often than their own M2+ event counts predict; Noto 2021-2023 was one of two such cases

## Summary

A long earthquake swarm in the Noto Peninsula (Japan) started in late 2020. An M 6.5 event occurred in the swarm area in May 2023, and the M 7.6 Noto Peninsula earthquake occurred there on 1 January 2024. After such a case, a frequent question is: does a long swarm tell us that a large earthquake is more probable? And is the increase larger than the number of swarm events alone predicts?

We tested this question with the public JMA unified hypocenter catalog for 1998-2024. An objective rule found all long (6 months or more) shallow sequences of M 2+ events in Japan. Then we counted how many of them were followed by an M 6.0+ event in their own area. We compared this count with four null expectations.

Main results (primary design):

* The rule found 27 long sequences. 26 were swarm-like (the largest event did not start the sequence). 8 of these 26 were possibly triggered by an earlier large event (all by the 2011 M 9.0 Tohoku-oki earthquake).
* 2 of the 26 swarm-like sequences were followed by an M 6.0+ event within 10 km of their area during the sequence or within one year: Niijima 1998-1999 (M 6.5 on 2000-07-01, at the start of the 2000 Miyakejima-Kozushima dike intrusion) and Noto 2021-2023 (M 6.5 on 2023-05-05; the M 7.6 followed on 2024-01-01). The fraction is 7.7% (exact 95% interval 0.9-25%).
* This count was 4.3 times the count expected from the mean Japanese areal rate of independent crustal M 6+ events (expected 0.47; one-sided p = 0.08). For the 18 swarm-like sequences that were not flagged as triggered, the factor was 6.0 (expected 0.33; p = 0.04).
* But the count was only 0.44 times the count expected if each M 2+ event of the sequence had the catalog-wide chance (0.00039) of being M 6+ (expected 4.5; 95% interval of the ratio 0.05-1.6). With the b-value of each sequence, the ratio was 0.48 (0.06-1.7). With the long-term M 2+ rate of the same areas at other times, the ratio was 0.80 (0.10-2.9).
* In 18 design variants, the ratio to the event-count expectation was 0.26-0.89 and was never significantly above 1. The ratio to the areal expectation was 2.4-8.1 and had p < 0.05 in 8 of 18 variants.
* Conclusion: long swarms raised the local chance of an M 6+ event compared with an average area of Japan. But the swarm event counts explain this increase. We found no extra precursor effect specific to swarms. The data permit at most about a 1.6-fold excess over the event-count expectation in the primary design (upper 95% bound).
* Only 2 of 33 independent crustal M 6+ events (6%, 95% interval 0.7-20%) had a long swarm-like sequence in their area before them.
* Exploratory, post hoc comparisons of duration, M 2+ count, largest magnitude, b-value, rate trend, timing of the largest event and depth did not clearly separate the two positive cases from the 24 others (two-sided Mann-Whitney p = 0.06-0.89 in the primary design; no feature had p < 0.05 consistently across variants). The two positive cases were among the longer and larger sequences, as the event-count explanation expects.

## Provenance and job information

* Campaign: 11_07_2026. Job: sci-1107-hp-earth-and-ocean-sciences-85ea61b5f8d1. Topic: earth-and-ocean-sciences. Machine: hp. Account: claude-andrii. Model: Claude Opus 5.5 (claude-opus-5-5), working as an autonomous research agent. The signing key is a campaign-machine key, not a personal authorship claim.
* Data: JMA unified hypocenter catalog yearly files h1998.zip-h2024.zip from https://www.data.jma.go.jp/eqev/data/bulletin/data/hypo/ . We used the copies in the campaign shared dataset store (`datasets/jma-hypocenter-hYYYY-20261109/hYYYY.zip`, downloaded 2026-11-09). We checked the SHA-256 of all 27 files that we used against the store provenance records. The exact names, sizes, SHA-256 values and URLs are in `files/provenance/jma_hypocenter_files.txt`.
* The record-level catalog is not in this bundle. `files/code/retrieve_and_run.sh` downloads (or copies) the files into a separate scratch folder and makes all results again. See `files/NOTICE-external-data.md` for the source terms and attribution.

## Data selection

* JMA 'J' records only (4,932,674 records in 1998-2024).
* Depth 25 km or less, 30-46 N, 128-146 E. We removed events with JMA region names that contain "FAR" (far offshore, low completeness). M 2.0 or more for detection: 193,075 events.
* Possible triggers: all JMA events with M 6.0 or more and depth 100 km or less in any region.
* The Aki-Utsu b-value of all selected M 2+ events is 0.76. This value is lower than the usual 0.9-1.0, probably because M 2.0 is not complete in all offshore areas. For this reason, the primary event-count null uses the empirical catalog fraction N(M >= 6.0) / N(M >= 2.0) = 75 / 193,075 = 0.00039, not a b-value.

## Method

1. Grid of 0.1-degree cells. Windows of 2 x 2 cells (about 22 x 18 km) on a 0.1-degree step. Monthly M 2+ counts for each window, January 1998 to December 2024.
2. Window background b = mean of the lowest 80% of its monthly counts. A month is active when its count is at least max(5, 4 b).
3. Episode = run of active months; a gap of one inactive month is permitted.
4. Episodes of overlapping windows that overlap in time are merged into one sequence. The sequence area is the union of its window cells.
5. Each sequence is cut before the first M 6.0+ event within 10 km of its area (search period: the sequence and 365 days after its last active month). Only sequences whose part before this cut lasts 6 months or more are kept ("long sequences").
6. Swarm-like: the largest event before the cut comes at least 7 days after the first event and after at least 10 events. Possibly triggered: an earlier M 6+ event lies within max(50 km, L) and max(365 days, 365 x 10^(0.5(M-7)) days) of the sequence, with L = 10^(0.5 M - 2) km.
7. Outcome: an M 6.0+ event within 10 km of the area during the sequence or within 365 days after its last active month.
8. Null expectations for each sequence i (p_i = 1 - exp(-E_i)):
   * E1 (areal): mean rate of independent crustal M 6+ events per km2 per year in all cells with M 2+ activity, times the buffered area and the outcome time. Independent events have no earlier M 6+ event within the trigger rule above (33 events).
   * E2 (local long-term): M 2+ rate of the same area outside the outcome window, times the outcome time and the catalog M 6+ fraction.
   * E3 (event count, primary null): number of M 2+ events in the area in the outcome window before any M 6+ event, times the catalog M 6+ fraction.
   * E3b: as E3, but with the Gutenberg-Richter fraction 10^(-b(6-2)) and the Aki-Utsu b of each sequence.
9. Test: the observed count O against the sum of independent Bernoulli(p_i) (Poisson-binomial; one-sided P(X >= O)). The interval of O/E is the exact Poisson 95% interval of O divided by E.
10. Sensitivity: 17 variants change one setting at a time: M 1.5 from 2004 and M 2.5 thresholds, count minimum 3 or 10, factor 3 or 6, gap 0 or 2 months, minimum duration 3 or 12 months, follow-up 180 or 730 days, Mbig 5.5 or 6.5, 3 x 3-cell windows, buffer 0 or 20 km.

We did not register these settings before the analysis. The first version of the code had two defects that we found and corrected before the final run: the trigger check used only the crustal subset (so the M 9.0 Tohoku-oki event, labelled "FAR E OFF MIYAGI", was missed), and the Aki-Utsu b of 0.76 made the event-count null too high. Both corrections made the event-count ratio nearer to 1 (from 0.23 to 0.44 in the primary design). The precursory features were first computed with the follow-up year included for sequences without an outcome; this biased the rate trend and we corrected it. The test results did not change.

## Results

### Long sequences of the primary design

| Start | Region (JMA name) | Active months | M2+ events (active) | Largest active M | Class | First M6+ in area |
|---|---|---|---|---|---|---|
| 1998-01-01 | NEAR NIIJIMA ISLAND | 20.9 | 579 | 5.2 | swarm-like | M6.5 on 2000-07-01 |
| 1998-01-01 | NW KAGOSHIMA PREF | 16.5 | 243 | 4.4 | swarm-like | - |
| 1998-05-01 | WESTERN NAGANO PREF | 7.9 | 47 | 3.3 | swarm-like | - |
| 1999-02-04 | SOUTHERN MIE PREF | 7.4 | 140 | 4.1 | swarm-like | - |
| 1999-04-04 | E OFF FUKUSHIMA PREF | 6.8 | 109 | 3.7 | swarm-like | - |
| 1999-05-05 | TOCHIGI GUNMA BORDER | 11.8 | 96 | 4.3 | swarm-like | - |
| 2000-12-01 | NORTHERN HYOGO PREF | 6.9 | 787 | 5.6 | swarm-like | - |
| 2001-01-03 | E OFF FUKUSHIMA PREF | 7.8 | 298 | 5.9 | swarm-like | - |
| 2001-05-16 | SOUTHERN NARA PREF | 10.3 | 138 | 4.1 | swarm-like | - |
| 2003-07-03 | NEAR NIIJIMA ISLAND | 12.9 | 319 | 4.4 | swarm-like | - |
| 2003-09-26 | SE OFF TOKACHI | 6.1 | 316 | 5.8 | not swarm-like | - |
| 2006-08-04 | MID NIIGATA PREF | 6.7 | 58 | 4.8 | swarm-like | - |
| 2011-03-11 | WESTERN FUKUSHIMA PREF | 32.4 | 2410 | 4.6 | swarm-like, possibly triggered (M9.0) | - |
| 2011-04-17 | SOUTHERN MIYAGI PREF | 7.4 | 112 | 3.4 | swarm-like, possibly triggered (M9.0) | - |
| 2012-08-03 | NORTHERN AKITA PREF | 8.7 | 94 | 4.9 | swarm-like, possibly triggered (M9.0) | - |
| 2013-08-13 | SW OFF KYUSHU | 6.5 | 73 | 4.1 | swarm-like | - |
| 2014-04-02 | E OFF FUKUSHIMA PREF | 6.9 | 350 | 5.0 | swarm-like, possibly triggered (M9.0) | - |
| 2017-03-02 | SATSUMA PENINSULA REGION | 10.9 | 179 | 5.3 | swarm-like | - |
| 2019-05-05 | NORTHERN IBARAKI PREF | 9.8 | 219 | 4.9 | swarm-like, possibly triggered (M9.0) | - |
| 2020-04-01 | HIDA MOUNTAINS REGION | 13.6 | 1064 | 5.5 | swarm-like | - |
| 2020-06-08 | E OFF FUKUSHIMA PREF | 13.7 | 366 | 5.3 | swarm-like, possibly triggered (M9.0) | - |
| 2020-10-02 | E OFF FUKUSHIMA PREF | 7.7 | 107 | 4.6 | swarm-like, possibly triggered (M9.0) | - |
| 2020-11-01 | SOUTHERN KUMAMOTO PREF | 7.9 | 68 | 4.4 | swarm-like | - |
| 2021-03-01 | E OFF FUKUSHIMA PREF | 20.0 | 633 | 5.0 | swarm-like, possibly triggered (M9.0) | - |
| 2021-05-05 | NOTO PENINSULA REGION | 23.9 | 1070 | 5.4 | swarm-like | M6.5 on 2023-05-05 |
| 2022-12-01 | E OFF FUKUSHIMA PREF | 25.0 | 817 | 5.0 | swarm-like | - |
| 2023-08-01 | E OFF BOSO PENINSULA | 6.8 | 122 | 5.4 | swarm-like | - |

The Niijima sequence starts at the catalog start (1 January 1998), so its true start is earlier. Several "E OFF FUKUSHIMA" sequences are shallow offshore activity near the plate interface, not crustal swarms on land.

### Observed / expected (primary design)

| Subset | Sequences | Followed by M 6+ | E1 areal | E2 local | E3 event count | E3b own b |
|---|---|---|---|---|---|---|
| All long | 27 | 2 | 4.04 (p 0.08) | 0.80 (p 0.75) | 0.43 (p 0.97) | 0.40 (p 1.00) |
| Swarm-like | 26 | 2 | 4.27 (p 0.08) | 0.80 (p 0.75) | 0.44 (p 0.97) | 0.48 (p 1.00) |
| Swarm-like, not triggered | 18 | 2 | 6.03 (p 0.04) | 1.32 (p 0.46) | 0.70 (p 0.83) | 0.72 (p 0.87) |

Values are O/E with one-sided p = P(X >= O). The full table for all variants and subsets is `files/results/culmination_tests.csv`.

### Across 18 design variants (swarm-like subset)

| Null | O/E range | Variants with p < 0.05 |
|---|---|---|
| E1 areal | 2.38-8.10 | 8 of 18 |
| E2 local long-term | 0.38-1.61 | 0 of 18 |
| E3 event count | 0.26-0.89 | 0 of 18 |
| E3b own b | 0.33-1.53 | 0 of 18 |

Some variants found other swarm-like positive cases: the 2016 M 7.4 and 2022 M 6.0 events after offshore Fukushima sequences, the 2007 M 6.8 Chuetsu-oki event, the 2016 M 6.3 northern Ibaraki event and the 2021 M 6.1 Tokachi-oki event (each in 2-4 of 18 variants). Noto was positive in all 18 variants. Niijima was positive in 13 variants; it was not positive with a 180-day follow-up, with no gap, with M 2.5, with a count minimum of 10, or in the 2004-2024 variant that does not include it (for Mbig 5.5, its outcome is the M 5.5 event of 2000-06-29).

### Figures

* `files/fig1_map.png`: map of the long sequences and the independent M 6+ events.
* `files/fig2_obs_exp.png`: observed / expected for all variants and the four nulls.
* `files/fig3_features.png`: features of the 26 swarm-like sequences; Noto marked.

## Interpretation

The areal null asks: "Is an M 6+ event more probable in a swarm area than in a random area of Japan?" The answer is probably yes (factor about 4, often significant). The event-count null asks: "Is an M 6+ event more probable than the number of small events in the swarm predicts, if each event has the same chance to be large?" The answer is no: the observed count was at or below this expectation in all variants. This agrees with models in which each earthquake has the same magnitude distribution and in which a large event is a random draw from the same population (for example, ETAS-type clustering models). It does not support a special swarm precursor effect beyond the event count. For hazard estimates, the M 2+ count of a swarm, with the regional magnitude distribution, gave an expectation that was not too low in this sample.

The Noto 2021-2023 sequence was long (92nd percentile of duration), had many events (96th percentile of active M 2+ count) and a large M 5.4 event, and its rate did not decrease (85th percentile of rate trend). But other sequences with similar or larger values, for example the Hida Mountains 2020-2021 swarm and the post-2011 western Fukushima swarm, had no M 6+ event.

## Limitations

* Only 2 positive cases in the primary design. The interval for the event-count ratio (0.05-1.6) cannot exclude a moderate excess, and it cannot exclude a large deficit.
* One positive case (Niijima/Kozushima, 2000) was a volcanic dike intrusion. The outcome M 6.5 came about 9 months after the end of the detected sequence.
* The detection rule is simple. It uses monthly counts in fixed windows, not a declustering model. Different rules find different sequences. We show 17 variants, but other rule families (for example nearest-neighbour clustering or ETAS residuals) can give other results.
* The trigger flag is approximate. Most post-2011 sequences in north-east Japan are flagged as possibly triggered by the M 9.0 event; the true causes are not known.
* Catalog completeness and the JMA processing changed during 1998-2024 (for example, more automatic solutions after 2016). M 2.0 is not complete in all offshore areas. The catalog M 6+ fraction (0.00039) includes all aftershock sequences.
* The sequences are not fully independent (several are in the same areas), and the null p values assume independence.
* The outcome window is fixed (365 days after the last active month). The 2024 M 7.6 event is inside the Noto window, but the outcome counts only the first M 6+ event.
* Crustal depth is set to 25 km or less. This includes some shallow offshore activity near plate interfaces.
* We did not register the analysis plan before we saw the data. The feature comparisons are exploratory.

## Reproduction

Requirements: Python 3.12 with numpy, pandas, pyarrow, scipy and matplotlib; bash, curl, unzip and sha256sum. Run:

```
bash files/code/retrieve_and_run.sh /path/to/scratch [/path/to/shared_datasets]
```

The script writes only into the scratch folder. It (1) gets the 27 JMA yearly files (from a local copy if given, else from JMA) and checks the SHA-256 values, (2) parses them (`parse_jma.py`), (3) selects the shallow events (`swarms.load_events`), (4) runs the primary design and all variants (`analyze.py`), and (5) makes the figures (`figures.py`). `posthoc.py OUTDIR` makes the exploratory feature table. The analysis step took 15-40 minutes of wall time on a shared 8-core machine with high load. We ran the script again from the shared copies into a new scratch folder: all 27 hashes matched, the parsed and selected event tables were identical to those of the original run, and the three result tables in `files/results/` were identical byte for byte. JMA can revise old files; if a hash differs, the script prints a warning, and results can change a little.

## Files

* `files/code/parse_jma.py`: parser for the JMA 96-column hypocenter format.
* `files/code/swarms.py`: sequence detection, merge, cut and classification.
* `files/code/analyze.py`: variants, null expectations and tests.
* `files/code/posthoc.py`: exploratory feature comparison.
* `files/code/figures.py`: figures.
* `files/code/retrieve_and_run.sh`: full reproduction into scratch.
* `files/results/sequences_all_variants.csv`: one row per long sequence and variant (sequence-level aggregates; derived from the JMA catalog).
* `files/results/culmination_tests.csv`: observed and expected counts, ratios, intervals and p values for all variants, subsets and nulls.
* `files/results/posthoc_features.csv`: exploratory feature comparisons.
* `files/results/summary_primary.json`: main numbers.
* `files/provenance/jma_hypocenter_files.txt`: source URLs, sizes and SHA-256 values.
* `files/NOTICE-external-data.md`: source and terms of the external data.

## License

`LICENSE` is the SCI baseline license (CC BY 4.0 for text, figures and data; MIT for code) for the materials that we made. The derived sequence tables are based on the JMA unified hypocenter catalog; see `files/NOTICE-external-data.md` for the source terms and the required attribution.
