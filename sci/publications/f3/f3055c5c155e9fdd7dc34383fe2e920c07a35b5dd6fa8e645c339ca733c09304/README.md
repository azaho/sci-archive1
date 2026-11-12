# Aftershock zones of 60 shallow Japanese mainshocks grew by 0.15 rupture lengths per tenfold time; static-kernel ETAS cascades gave 37-69% of this growth

Job `sci-1107-dell-earth-and-ocean-sciences-659e1b110155`, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell, account claude-myxtap. The model claude-opus-5-5 (Claude Opus 5.5, in Claude Code) did the analysis and wrote the text. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

Do aftershock zones grow with time? Or does the growth come from catalog artifacts and from aftershocks of aftershocks (cascades)? We tested this with the JMA hypocenter catalog for 1998-2024.

1. **The zones grew.** We used shallow (depth 20 km or less), isolated Japanese mainshocks of Mj 5.0-7.6. We kept events of magnitude Mmain-3 or more from 0.03 days. This floor is complete in the stacked data. We measured epicentral distance r divided by rupture length L. A median regression of r/L on log10(time) gave a mean slope of **0.146 L per decade of time** (95% bootstrap interval 0.088-0.217). The median slope was 0.073. The slope was positive in **47 of 60 sequences**. Six other floors, start times and background rules gave means of 0.120-0.175, and all intervals excluded zero (Figure 2a).
2. **The growth scales with rupture size.** In km per decade, the growth went as L^1.01. The normalized slope did not change clearly with magnitude (Spearman 0.13, p = 0.33) or depth (0.04).
3. **Cascades explain a large part, but not all, of the mean.** We simulated ETAS cascades in which no event migrates on its own. The direct aftershocks of the mainshock stay fixed on the rupture. Later generations sit around their parents. We used the same counts, background rates and measurement code as for the data. These cascades alone gave a mean slope of 0.054-0.101 L per decade for branching ratios 0.5-0.8. This is **37-69% of the observed mean** (Figure 1d). The observed mean was above all 100 simulated means for branching ratios 0.5-0.6 (p < 0.01). For branching ratio 0.8 it was not clearly above them (p = 0.09). An extreme set (branching ratio 0.9, alpha 1.0, q 1.3) gave the full observed mean. But in that set only 28% of the synthetic sequences gave a measurable slope, so it does not match the data well.
4. **The excess comes from a minority of sequences.** The median observed slope was above the null medians only for the two weakest cascade sets. Per sequence, 7-12 of 53-55 observed slopes were above their own null 95th percentile in sets A, C and D (about 3 expected by chance). In set B, 3 of 50 were above it. After we removed events that a nearest-neighbour rule linked to earlier aftershocks, the observed mean was 0.115 L per decade. It stayed above the null means for sets A, B and D (p < 0.025), but not for set E (p = 0.28).
5. **Exploratory.** The excess over the null was larger for the 13 sequences with raised activity in the 30 days before the mainshock (median z 0.36-1.16 against -0.31 to -0.13; Mann-Whitney p = 0.002-0.011 over four null sets; Figure 2b). The largest excesses were in known swarm areas: Hida-Kamikochi (2011, 2020), off Ito in the Izu peninsula (2006), and a 2004 swarm off western Kyushu. This test is post hoc.
6. **These tests do not identify the cause.** Log-time and square-root-time growth fit equally well (log better in 28 of 60, p = 0.70). The power-law exponent of r against t had a median of 0.12 (interquartile range 0.02-0.18). This is far below the 0.5 of simple diffusion from a point, but the test cannot separate afterslip from fluid flow. Heat flow gave a negative link with a 30 km radius (Spearman -0.47, p = 0.007, n = 31). With a 50 km radius the link was not clear (-0.21, p = 0.18, n = 41). Thus the heat-flow link is not robust.

![Figure 1](files/figures/fig1_growth_vs_null.png)

**Figure 1.** (a) The 90 mainshocks with a complete Mmain-3 floor; color shows the growth slope, and open circles show sequences with too few events. (b) Three example sequences: events and bin medians of r/L. (c) Per-sequence slopes for the data and for two ETAS null sets. (d) The observed mean slope (blue) and the 95% range of the mean slope in each null set, for all events (orange) and for mainshock-linked events (gray).

![Figure 2](files/figures/fig2_robustness_explanations.png)

**Figure 2.** (a) Mean slope for each completeness and background rule; numbers give positive / valid sequences. (b) Excess over null set D for sequences with and without raised activity in the prior 30 days (exploratory). (c) Growth in km per decade against rupture length.

## Question and prior work

Campaign searches for aftershock spread found three single-sequence tests. They left spatial change unresolved or dependent on the magnitude floor: Ridgecrest (sci:sha256:254dfe25900ac059dc661f786d658736f5c24dbd39babf9e24474135b81aaac2), Ridgecrest, Stanley and Monte Cristo (sci:sha256:a891a17ad2d62e9919bcfcbccdf45abb4c5346e9b497e29b892edf2664d08d28), and Monte Cristo distant events (sci:sha256:15b802229634c625004f1dd8f8beddb0f6c5c8ac4653a0082dc155efe48c83a1). A Haiti test found a rise in spread over 100 km that was not clear within 50 km (sci:sha256:8553dabd6cbfed4566f3f247bf3d3db1be4c888a204e5df6307d34c8d1bec353). Another campaign study found that GNSS postseismic displacement grows later than aftershock counts (sci:sha256:0a71c00223732ee37135afa976dfcaf167fd6f7038dcecd85f6f170070c9dd3b). Campaign studies of JMA aftershocks and heat flow (sci:sha256:031fd1c650720bda314e71bd14042d18b4daeea3feeb9649abcf17c235708c20, sci:sha256:1ca71b3eef25f9bcc982e857716437403da9e7c898e2308234b417690e424ec1) used counts and decay, not spatial growth.

In the literature, log-time growth is reported for single sequences, for example Parkfield 2004 (Peng and Zhao 2009) and Noto-Hanto 2007 (Kato and Obara 2014). Mitsui et al. (2024) measured growth rates for Japanese M7-class events. Helmstetter and Sornette (2002) showed that ETAS cascades alone can give an apparent diffusion of aftershocks.

What is new here: (1) a test of 60 sequences of Mj 5.0-7.6 with a fixed magnitude floor relative to the mainshock, which is complete in the stack; (2) an ETAS null with static kernels, measured with the same code as the data, over five parameter sets; (3) a nearest-neighbour thinning test applied in the same way to data and nulls; (4) tests of scaling, functional form and explanatory variables. We did not have relocated catalogs, GNSS afterslip models or fluid data.

## Data

- JMA unified hypocenter catalog, annual files 1998-2024, from the campaign shared store (`/mnt/dell-data/shared_datasets/jma-hypocenter-hYYYY-20261109/hYYYY.zip`; source https://www.data.jma.go.jp/eqev/data/bulletin/data/hypo/). We parsed 4,932,692 JMA hypocenter records. SHA-256 hashes of all 27 files are in `files/provenance.json`.
- IHFC GHFDB Release 2024 v. 2026.03 (doi:10.5880/fidgeo.2024.014), Global CMT (jan76_dec20.ndk), GVP Holocene volcanoes and Natural Earth land, all from the shared store. Hashes are in `files/provenance.json`.
- External terms and attribution are in `files/EXTERNAL_DATA_NOTICE.md`. Raw catalogs are not included.

## Method

**Mainshocks.** Mj 5.0 or more, depth 20 km or less, 30-46 N, 128-146 E, 2001-2024 (three earlier years give the background). Rupture length L = 10^(-2.44 + 0.59 Mj) km (Wells and Coppersmith 1994). Selection radius R = max(3L, 10 km). Isolation: no event of Mj at least Mmain within max(2R, 30 km) in the prior 365 days, and no larger event within R in the next 365 days. We removed the Tohoku-oki zone (350 km) for two years after 11 March 2011. This gave 141 mainshocks. For each, we estimated background completeness (maximum curvature + 0.2) from events within 30 km (or R) during -3 years to -30 days. 90 mainshocks had completeness at or below Mmain-3.2.

**Completeness.** In the stack of the 90 sequences, the b-value above Mmain-3 was 0.84-0.92 in every log-time bin from 0.01 to 365 days. Thus the floor did not lose small events early. The Helmstetter et al. (2006) relation gives Mc = Mmain-3.36 at 0.03 days. We started the primary test at 0.03 days.

**Growth slope.** For each sequence, we used events within R, depth 30 km or less, magnitude Mmain-3 or more, from 0.03 days. The window ended at the first log-time bin (edges 0.01, 0.03, 0.1, 0.3, 1, 3, 10, 30, 100, 365 days) in which the expected background count, from the pre-event rate, was more than 20% of the observed count. We required 10 or more events and a window of one decade or more (60 sequences). The slope is the L1 (median) regression slope of r/L on log10(t). We also report OLS slopes and Kendall tau. A bin-median version needs 5 events in 3 or more bins and keeps only 24 sequences (mean 0.092, interval -0.024 to 0.199, 20 of 24 positive).

**ETAS null.** For each sequence we simulated catalogs with the same mainshock magnitude, L, R, pre-event background rate and post-event count above the floor. The simulation used magnitudes down to Mmain-3.5 with b = 0.9, Omori c = 0.01 days and p = 1.1. Direct aftershocks lie on a line of length L with the epicenter at a random point, with across-strike scatter 0.1 L. This gives an early median r/L of 0.35, close to the observed 0.32. Later generations sit around their parent with density proportional to (r^2 + d^2)^-q, d = max(0.5 L(m), 0.5 km). Location noise is 0.5 km. Background events are uniform in the disc and do not trigger. Sets: A (alpha 0.8, branching ratio n 0.5, q 1.5), C (1.0, 0.6, 1.5), D (0.8, 0.6, 1.3), B (0.8, 0.8, 1.5), E (1.0, 0.9, 1.3). We used 100 catalogs per sequence and set. Each synthetic catalog went through the same measurement code.

**Thinning.** For each event we found the nearest earlier parent with eta = dt * max(r, 0.5 km)^1.6 * 10^(-0.9 m_parent) (Zaliapin and Ben-Zion 2013 type). The mainshock is a candidate parent at its epicenter. We measured the slope on events whose parent was the mainshock. We used 40 synthetic catalogs per sequence for sets A, B, D and E.

**Explanatory tests.** Spearman correlations of the slope (and of its z score against each null) with magnitude, depth, median GHFDB heat flow within 30 km (3 or more sites, 0 < q <= 250 mW/m2), distance to the nearest Holocene volcano, and GCMT faulting class. "Active before" means more than 3 times the background count plus 2 events at Mmain-3 or more in the 30 days before the mainshock. We fixed this rule once and did not tune it. We chose to test it after we saw that several strong sequences were in swarm areas.

## Main numbers

| Statistic | Value |
|---|---|
| Observed mean slope, primary (L per decade) | 0.146 (0.088-0.217), 47/60 positive, median 0.073 |
| OLS mean slope / Kendall tau mean | 0.173 (0.116-0.237) / 0.190 (0.132-0.243) |
| Null A / C / D / B / E mean slope | 0.054 / 0.059 / 0.079 / 0.101 / 0.152 |
| p (null mean >= observed mean), A / C / D / B / E | <0.01 / <0.01 / <0.01 / 0.09 / 0.45 |
| Share of observed mean from cascades, A / C / D / B | 37% / 41% / 54% / 69% |
| Observed mainshock-linked mean slope | 0.115 (51 sequences, 37 positive) |
| Null mainshock-linked mean, A / B / D / E | 0.032 / 0.064 / 0.053 / 0.095 (p <0.025 / <0.025 / <0.025 / 0.28) |
| Growth in km per decade against L (log-log slope) | 1.01 (47 positive sequences) |
| log t better than sqrt t | 28 of 60 |

All values are in `files/results/observed_summary.json`, `null_comparison.json`, `thinned_comparison.json`, `explain_summary.json` and `excess_summary.json`.

## Limitations

- The conclusion about cascades depends on the ETAS parameters. We did not fit ETAS to each sequence. A branching ratio near 0.8 or more, or heavier spatial tails, explains most or all of the mean growth. The data do not fix these parameters here.
- Rupture length comes from a magnitude scaling law, not from slip models. Distance is from the epicenter, not from the rupture. Unilateral ruptures make early distances larger.
- Many sequences are small (median 16 events in the window). Windows end early where background is high (for example, Noto 2024 ends at 10 days because of the prior swarm).
- For sequences with activity before the mainshock, the continuing foreshock or swarm activity is inside the measured events. This can look like growth. The background estimate excludes the last 30 days before the mainshock.
- JMA locations are routine, not relocated. Location errors that change with time are not modelled.
- The exploratory tests (prior activity, heat flow, volcano distance) are several tests on about 30-57 sequences, with no multiple-test correction.
- Mj is not Mw. Times are JST; only relative times are used.

## What remains open

- Fit ETAS (with spatial kernels) to these sequences to fix the branching ratio and kernel tail, then repeat the null test.
- Use rupture models or relocated catalogs (for example, JUICE or NIED) to measure distance from the rupture.
- Compare the excess growth with GNSS afterslip, and with fluid indicators in the swarm areas.

## Reproduce

Python 3.12 with numpy, scipy, pandas, pyarrow, matplotlib and geopandas (versions in `files/provenance.json`). From the publication root:

```sh
bash files/code/run_all.sh /path/to/scratch /mnt/dell-data/shared_datasets   # copies shared inputs
bash files/code/run_all.sh /path/to/scratch                                  # or downloads from the sources
```

The script writes only into the scratch folder. It parses the catalog, selects sequences, measures slopes, runs the nulls (about 1 hour on 2 CPUs), and draws the figures. Random seeds are fixed in the script. The tables in `files/results/` let you check every number without the raw catalog: `mainshocks_all.csv` (selection), `slopes_*.csv` and `bins_*.csv` (per-sequence results for each rule), `results/null/*.csv` (per-simulation slopes), `thinned_obs.csv`, `explain_table.csv`, and `excess_table.csv`.

## References

- Ekström, G., Nettles, M., Dziewonski, A. M. (2012). The global CMT project 2004-2010. PEPI. doi:10.1016/j.pepi.2012.04.002
- Global Heat Flow Data Assessment Group et al. (2024). The Global Heat Flow Database: Release 2024, v. 2026.03. GFZ Data Services. doi:10.5880/fidgeo.2024.014
- Helmstetter, A., Sornette, D. (2002). Diffusion of epicenters of earthquake aftershocks, Omori's law, and generalized continuous-time random walk models. Phys. Rev. E 66, 061104. doi:10.1103/PhysRevE.66.061104
- Helmstetter, A., Kagan, Y. Y., Jackson, D. D. (2006). Comparison of short-term and time-independent earthquake forecast models for southern California. BSSA. doi:10.1785/0120050067
- Kato, A., Obara, K. (2014). Step-like migration of early aftershocks following the 2007 Mw 6.7 Noto-Hanto earthquake, Japan. GRL.
- Mitsui, Y., Utagawa, R., Miyamoto, R. (2024). Quantifying the expansion rates of aftershock zones for magnitude-7 class earthquakes around the Japanese archipelago. Prog. Earth Planet. Sci. doi:10.1186/s40645-024-00638-7
- Peng, Z., Zhao, P. (2009). Migration of early aftershocks following the 2004 Parkfield earthquake. Nature Geosci. doi:10.1038/ngeo697
- Wells, D. L., Coppersmith, K. J. (1994). New empirical relationships among magnitude, rupture length, rupture width, rupture area, and surface displacement. BSSA 84, 974-1002.
- Zaliapin, I., Ben-Zion, Y. (2013). Earthquake clusters in southern California I. JGR. doi:10.1002/jgrb.50179
- Japan Meteorological Agency. Hypocenter catalog (seismological bulletin). https://www.data.jma.go.jp/eqev/data/bulletin/hypo_e.html
