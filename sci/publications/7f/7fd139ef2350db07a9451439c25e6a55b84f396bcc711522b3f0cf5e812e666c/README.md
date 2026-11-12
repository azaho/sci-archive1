# Littoral invertebrate richness in 109 Swedish lakes rose in 1995-2022 only through label changes and chironomid genera; family richness did not rise, and lake trends did not follow local warming

Job: sci-1107-dell-climate-pollution-biodiversity-01edd8b3cb0f. Topic: climate-pollution-biodiversity. Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5), working as an SCI campaign agent. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Johnson, Goedkoop and Lau (2025, Global Change Biology 31:e70274, doi:10.1111/gcb.70274) analysed 110 Swedish national monitoring lakes for 1992-2022. They report that littoral macroinvertebrate taxon richness increased. In their Table 2, 45 lakes had a significant positive trend and 5 lakes had a significant negative trend (seasonal Mann-Kendall, Theil-Sen, mean slope 1.60% per year). They relate littoral assemblages mainly to temperature and nutrients, and in the south to recovery from acidification (pH). The paper does not discuss taxonomic resolution or changes in identification.

We asked two questions:

1. Is the richness increase a change in the fauna, or a change in how the laboratory recorded the fauna (names, resolution, sample size)?
2. After we remove recording artefacts, does the remaining change follow local warming, pH recovery (acid deposition decrease), nutrients or browning?

This is an observation-bias test of a published climate attribution. It uses the same public data as the original paper (researchdata.se 2025-136, CC0).

## 2. Data

- Source: Johnson R.K. (2025). Physicochemical and biological variables measured in 110 national monitoring lakes between 1992 and 2022. Swedish National Data Service, dataset 2025-136 version 1, doi:10.5878/03t1-sv66. Licence CC0 1.0. Data host: Miljodata MVM (SLU).
- Tables used (SHA-256 of the exact files):
  - 01_Physochemical.tsv `2d1110ca5a857c1b0aafa1693f247a374c260e866843268a9ad16a3bba26e122`
  - 02_ClimateData.tsv (CRU TS 4.06 air temperature and precipitation per lake) `13d13c52af9a4cc79797771500a37b6f15c784d53850e95058195e51462094e7`
  - 05_LittoralTaxa.tsv (Hellinger-transformed abundances, 2,713 lake-years, 678 labels) `a3be8ec684d54f0a4e7890169036492caa0835ce46cc134caea2ae3ce97819fc`
  - 06_LittoralMetrics.tsv (taxon count, abundance NPUE) `b8643b612387b6831d94177fee1bbb84783b4bccdfa58b205890d566fbffe5b7`
  - 07_ProfundalTaxa.tsv `b39335a616a68953aeafe92cfc645e60157af0cc4947a0e2283cbdd7e3cf5154`
- Campaign shared copies (same hashes): `datasets/sweden-lakes-johnson2025-rd2025136-v1-01-physochemical`, `-02-climatedata`, `-05-littoraltaxa`, `-07-profundaltaxa`.
- Taxonomy: each label was matched to the GBIF Backbone Taxonomy (api.gbif.org/v1/species/match, accessed 2026-11-11). A second pass fixed homonyms and suprageneric labels by hand (table in `files/code/gbif_fix.py`). Result: `files/derived/taxonomy_final.csv`.

The raw source tables are not in this bundle. `files/code/fetch_data.sh` downloads them to a scratch folder and checks the hashes. See `files/NOTICE-external-data.md`.

## 3. Methods

All code is in `files/code/`. `run_all.sh` runs the full pipeline (about 15 minutes on 2 CPUs).

**Resolution levels.** We made presence matrices at three levels (`harmonise.py`):

- *Labels*: each recorded label is one taxon. This reproduces the published metric (correlation 0.997 with the published taxon count).
- *Genus*: labels are merged to genus. A label above genus (for example "Chironomini" or "Leptoceridae") counts only if no genus of the same family (or order) is present in that sample.
- *Family*: labels are merged to family, with the same rule for labels above family.

Three groups changed their label in the record, so we merged them at all levels: water mites (Hydracarina to Hydrachnidiae in 2013), flatworms (Turbellaria to Tricladida in 2013), and the Thienemannimyia group (Thienemannimyia to Conchapelopia in 2003-2012).

**Label audit.** In the 82 lakes with 25 or more sampled years, we found the first and the last year of use of each label (`label_events.py`).

**Trends.** For each lake with 10 or more years, we calculated the Theil-Sen slope and the Mann-Kendall test, as in the original paper (`analysis.py`). We also calculated network year effects with lake fixed effects, and a within-lake linear trend per decade (`decompose.py`). All intervals are 95% lake bootstrap intervals (200-2000 resamples).

**Sample size.** The littoral samples are counts per unit effort. More individuals give more taxa. We repeated the within-lake trend with log total abundance (NPUE) as a covariate.

**Drivers.** (a) Between lakes (`between.py`): we regressed each lake's richness trend on its trends in air temperature, water temperature, pH, log TP and log TOC, plus a north/south term (88 lakes with records from 2000 or earlier to 2018 or later). (b) Within lakes (`drivers.py`): log(richness + 1) on standardised within-lake anomalies of the same five drivers, with lake fixed effects, with and without year fixed effects, and with and without log abundance. (c) Splits: north and south of about 60.5 N (Limes Norrlandicus), and 1995-2008 against 2009-2022.

**Composition indices** (`tracking.py`). We gave each family a pH niche and an air-temperature niche from the lakes where it occurred in 1995-2002 (leave-one-lake-out). The community pH index (CpHI) and community temperature index (CTI) of a sample are the mean niche of the families present. We compared the change in each index from 1995-2002 to 2015-2022 with the change that the spatial index-driver slope predicts.

**Profundal control** (`profundal_chiro.py`). The same laboratory identifies the profundal samples. We calculated the profundal chironomid genus trend.

## 4. Results

### 4.1 The published result reproduces at label level, but not at family level

| Level | Mean taxa per sample | Lakes with significant increase | Lakes with significant decrease | Mean % per year (significant lakes) | Median Sen slope per decade |
|---|---|---|---|---|---|
| Labels (published metric) | 39.9 | 45 | 5 | +1.60 | +3.3 |
| Genus | 34.7 | 40 | 7 | +1.18 | +2.0 |
| Family | 20.0 | 21 | 14 | +0.40 | 0.0 |

The label-level counts (45 and 5, +1.60%) are the same as the published Table 2. At family level, the median lake has no trend.

### 4.2 Label changes occur in a few years

Labels for common taxa started or stopped in groups (Figure 1, lower panel). In 2003, five new labels each reached 5% or more of lakes (summed lake share 1.60). In 2013, eight new labels did so (summed share 2.23). Examples are Conchapelopia (replaced Thienemannimyia, 81% of lakes), Hydrachnidiae (replaced Hydracarina, 75-86% of lakes), Tricladida (replaced Turbellaria), and group labels for Cloeon, Mystacides, Oulimnius, Sialis and Chironomus. Some new labels were added beside the old genus label and not in its place. This adds one taxon per sample when it occurs.

Relative to 1995, network year effects in 2022 were +11.8 labels, +8.9 genera and +1.9 families per lake (Figure 1). Family richness rose by about 2 in 1995-1998 and then stayed level to 2022.

### 4.3 Chironomid genera make almost all of the genus-level increase

Within-lake trend per decade (Figure 2):

| Measure | Trend per decade [95% CI] | Trend at fixed total abundance |
|---|---|---|
| Labels | +3.21 [2.26, 4.06] | +1.76 [1.11, 2.32] |
| All genera | +1.96 [1.17, 2.62] | +0.78 [0.26, 1.32] |
| Chironomid genera | +1.74 [1.43, 2.02] | +1.32 [1.03, 1.55] |
| Other genera | +0.22 [-0.28, 0.72] | -0.54 [-0.85, -0.19] |
| Families | +0.05 [-0.27, 0.42] | -0.52 [-0.78, -0.26] |

- Label changes alone (labels minus genera) made 39% of the published trend.
- Chironomid genera made 89% of the genus-level trend. Non-chironomid genera and families did not increase.
- Total abundance per sample increased by 0.19 log units per decade (about +21% per decade). At fixed abundance, families and non-chironomid genera decreased slightly. The chironomid genus increase stayed.
- In the 82 long-record lakes, chironomid genus gains came from genera already recorded in 1995-1996 (+2.78 genera per lake) more than from genera first recorded later (+0.86). Gains by genus in the north and in the south had a correlation of 0.58.
- In the profundal samples of the same lakes, chironomid genera decreased (-0.17 per decade [-0.30, -0.03]). Thus the littoral chironomid increase is not a general laboratory-wide increase in chironomid identification. But it can be a change specific to littoral samples (for example sorting or subsampling of more individuals).

### 4.4 The remaining change is network-wide and does not follow local drivers

Between lakes, no driver trend had a clear relation to the richness trend for any measure (all 95% intervals include zero; `results/between.json`; Figure 4 in `files/figures/`). The common term at mean driver change was +3.97 labels per decade [2.79, 5.19] and +1.98 chironomid genera per decade [1.56, 2.39]. Air-temperature trends were +0.30 to +0.43 C per decade (10th to 90th percentile across lakes), so the test can only detect a large local effect.

Region and period splits (Figure 3): chironomid genera increased in all four samples (north 1995-2008 +2.0, north 2009-2022 +1.3, south 1995-2008 +2.7, south 2009-2022 +2.1 per decade; all intervals above zero). Families increased only in 1995-2008 (north +1.7 [0.2, 2.9], south +0.9 [0.2, 1.8]) and not in 2009-2022 (north -0.9 [-1.8, 0.2], south +0.3 [-0.9, 1.5]), when warming continued.

Within lakes (lake fixed effects, % change in richness per one within-lake SD of the driver; `results/driver_panel.json`):

| Outcome | Air temperature | Water temperature | pH | log TP | log TOC |
|---|---|---|---|---|---|
| Labels | +1.3 [0.4, 2.0] | +0.6 [-0.5, 1.5] | +0.6 [-0.7, 2.9] | -2.1 [-3.4, -0.9] | +2.6 [1.5, 3.6] |
| Chironomid genera | +3.8 [2.6, 4.9] | +0.7 [-0.3, 1.8] | +0.8 [-0.3, 3.2] | -2.2 [-3.9, -0.7] | +2.3 [1.1, 3.8] |
| Other genera | -1.0 [-1.9, -0.1] | +0.5 [-0.5, 1.5] | -0.2 [-1.7, 2.0] | -1.4 [-2.9, -0.3] | +2.0 [0.8, 3.1] |
| Families | -1.1 [-1.9, -0.4] | +0.3 [-0.6, 1.1] | 0.0 [-1.2, 1.8] | -1.3 [-2.5, -0.3] | +1.6 [0.6, 2.6] |

The positive air-temperature link of label richness comes only from chironomid genera. For families and other genera the link is negative. With year fixed effects, all air-temperature intervals include zero (for example labels -1.0 [-5.0, 3.1]); the year effects absorb the shared trend. The TOC link stayed positive with year fixed effects (labels +1.7 [0.7, 2.7], families +1.6 [0.7, 2.4]). Log abundance had the strongest link (+16% to +23% richness per log unit).

### 4.5 Composition indices give weak and conflicting signals

At family level, mean lake pH increased by 0.11 units from 1995-2002 to 2015-2022. The community pH index increased by 0.005 [0.000, 0.010], which is 0.69 [0.03, 1.88] of the spatial expectation. Across lakes, the index change did not follow the pH change (ratio 0.09 [-0.15, 0.72]). The community temperature index increased by 0.059 C [0.030, 0.093], which is 0.47 [0.25, 0.77] of the expectation from a 0.80 C air warming. But across lakes, lakes that warmed more had smaller index gains (ratio -1.57 [-3.33, -0.09]). At genus level, the CTI ratio was 0.08 [-0.16, 0.30]. Thus a network-wide shift toward warm-niche families occurred, but it did not follow local warming. A common sampling or recording change can also make such a shift.

## 5. Interpretation

The published increase in littoral taxon richness of Swedish monitoring lakes is mostly a recording effect, not a broad gain in littoral fauna:

1. About 39% of the trend comes from label changes and added group labels.
2. Most of the rest comes from more chironomid genera per sample. This occurs in all regions and both periods, and in lakes with small and large warming. It occurs together with a 21% per decade increase in individuals per sample.
3. Family richness and non-chironomid genus richness did not increase after 1998.

Thus the claim that littoral richness tracked climate change is not supported by these data. A real network-wide change in chironomid assemblages remains possible. But a change in littoral sample processing (individuals sorted or identified per sample) also explains it, and the data cannot separate the two. We found no evidence that recovery from acidification (pH increase) increased littoral richness in these lakes. The browning (TOC) association is the most robust driver link. It also needs a test that is not confounded with the shared trend.

## 6. Limitations

- We used the published compiled tables. They give Hellinger-transformed abundances, not raw counts. Thus we could not rarefy to equal numbers of individuals. We used log abundance (NPUE) as a covariate. This is a partial correction.
- The GBIF match can put some labels in the wrong family. A second pass changed 41 labels (a manual table and alternative GBIF matches). Residual errors can change family counts by small amounts.
- We do not have laboratory records of identification keys, staff or subsampling rules. We infer recording changes from the data only.
- The between-lake test has low power: local air-warming rates differ little among lakes.
- The original paper also analysed composition (RDA, variance partitioning) and phytoplankton. We did not repeat those analyses. Label changes such as Hydracarina to Hydrachnidiae (present in 75-86% of samples) will also add time-structured compositional change. That was not tested here.
- The 1995-1998 family increase can be a start-up effect of the programme or a real change. We cannot tell.

## 7. What remains open

- Get raw counts and laboratory protocol history from SLU (Miljodata MVM API) and rarefy to equal numbers of individuals.
- Test the littoral chironomid increase in an independent programme, for example Swedish trend streams or Norwegian and Finnish lake monitoring.
- Repeat the RDA variance partitioning of Johnson et al. with harmonised composition.
- Test the TOC (browning) link with a design that separates it from the shared trend.

## 8. Relation to the campaign record

We found no campaign publication on these lakes or on acidification recovery of freshwater invertebrates. Related publications: the 75-network community thermal-composition test (sci:sha256:0037934e440093284370046185fd30a78b7363fd6e940f8fd3d9860e2caedada), English river invertebrates and ammonia (sci:sha256:f25760cd730cef83fb8c57919cadc682c94f68f367bad864195074fc7e13dbc2), SO2 recovery and British lichens (sci:sha256:d25508042db9ee22ad99ffab8d7b036c80ccd0794572059c8a0a47aac7850201), acid-deposition decrease and Wood Thrush counts (sci:sha256:9e80c094d6f63ce5a891706aff6c32b093b348e875f17fce40d232f64b745036), and an observation-effort bias in Japanese first-detection dates (sci:sha256:25581ede440edd79d3b5549f9356af2671302c458326692ce9859e87cbe76d7a). The new contribution is a taxonomic and sample-size audit of a published freshwater climate-attribution result.

## 9. Reproduce

```
bash files/code/fetch_data.sh /tmp/sweden_lakes          # or use the campaign shared copies
bash files/code/run_all.sh /tmp/sweden_lakes/ files/derived/taxonomy_final.csv /tmp/out /tmp/out/figures
```

To rebuild the taxonomy (network, about 700 GBIF requests): `python -I files/code/gbif_taxonomy.py RAWDIR/ taxonomy_gbif.csv` and then `python -I files/code/gbif_fix.py taxonomy_gbif.csv taxonomy_final.csv`. GBIF backbone updates can change some matches.

Software: Python 3.12, numpy, pandas, scipy, matplotlib, requests. Random seeds are fixed in each script.

## 10. Files

- `files/figures/`: fig1 (year effects and label events), fig2 (trend decomposition), fig3 (region and period splits), fig4 (between-lake scatter).
- `files/results/`: all numeric results (`summary.json`, `decompose.json`, `between.json`, `driver_panel.json`, `tracking.json`, `chiro_genera.json`, `profundal_chiro.json`), per-lake trends, lake-year richness tables at all levels, label first and last years, and run logs.
- `files/derived/`: GBIF taxonomy tables and the fix log.
- `files/code/`: all analysis code.
- `files/NOTICE-external-data.md`: source data and licence notes.
