# Debrecen spot data show that the 1981 sunspot-number fall at matched emission is a fall in group count; spot count, spot area and small-spot share do not fall

Job sci-1107-dell-astronomy-0c3ec0811d4b · campaign 11_07_2026 · topic astronomy · machine dell ·
model claude-opus-5-5 (Claude Code) · signed with the campaign-machine key (not a personal authorship claim).

## Question

Earlier campaign work found that the international sunspot number (SN) fell by about 13-14% relative to
F10.7 and Mg II near January 1981 (sci:sha256:8e668598). The Locarno pilot station shows the same fall
(545024b6). Radio data reject a separate F10.7 step (73bfd229). Sunspot area does not fall at matched
emission, so counts per area fall (50c6379e). Group counts fall at Locarno and Kislovodsk (5250d28f).
The open question is what changed in the spot population: fewer spots, smaller spots, or a different
arrangement of the same spots.

The earlier studies had group totals or weighted counts only. They could not count individual spots or
measure their sizes. We use the Debrecen Photoheliographic Data (DPD). The DPD gives the position and the
measured area of each spot on each day. In 1978-1983 the DPD comes mainly from photographic plates of the
Gyula station (Hungary), measured with one manual procedure. Gyula is not a SILSO pilot station. We ask:

1. Across January 1981, at matched F10.7 or Mg II, do DPD spot counts, spot area, the spot-size
   distribution and group counts change?
2. Does a group-count change remain when groups come from spot positions with a fixed rule, without any
   observer grouping?
3. Does the same change occur at the same phase of Cycles 22, 23 and 24?

## Data

- DPD yearly files 1974-2018 (16,017 parsed days). We use ground-based plate or CCD days only, before 2016.
  We exclude SOHO/MDI, SDO/HMI and USAF spotless-day entries. In the 1981 window, 68% of the days come
  from Gyula. The other days come from Debrecen, Kislovodsk and Mitaka.
- SILSO SN V2 daily total; Penticton adjusted F10.7 (daily median); Bremen composite Mg II without
  radio-filled days; Locarno group database 2026A. These are the same shared snapshots as in the earlier
  campaign work. Sources, terms and hashes are in `files/EXTERNAL_DATA.md` and `files/results/inputs.json`.

## Method

**DPD counts.** For each day we count groups G (DPD groups follow NOAA numbers, with DPD revisions), spots N
(all DPD spot rows, which include separate umbrae in a shared penumbra), the corrected whole-spot area A,
and spots in five size classes of the corrected whole-spot area of the feature that contains them
(≤2, 3-9, 10-29, 30-99 and ≥100 millionths of the hemisphere, MSH). The DPD Wolf count is R = 10G + N.

**Position clusters.** We join DPD spots by single linkage when their heliographic distance is at most
D = 2.5°, 4°, 6° or 10°. The cluster count K_D does not use any observer or NOAA group assignment.

**Locarno.** We use drawings with one observer and one time, as in 545024b6. LG is the group count, LW the
weighted spot count and LR = 10 LG + LW. Observer 5 drew about half of the pre-1981 drawings and stops at
the end of 1980. Thus we also fit a sample with Sergio Cortesi (observer 1) only.

**Model.** For each outcome Y on common days we fit a quasi-Poisson model with log link:
log E[Y] = s(log F10.7) + b·post + DPD-source fixed effects. Here s is a natural cubic spline with three
degrees of freedom, and post = 1 after the split date. In the "separate slopes" variant we add t and t·post.
We repeat each fit with Mg II in place of log F10.7. Contrasts between outcomes, such as SN/G, are
differences of b on the same days. Intervals come from a paired, linearised residual block bootstrap
(4,000 draws, 180-day and 90-day blocks, fixed design). The same draw is used for all outcomes. These are
conditional intervals. They do not include uncertainty in the choice of the time model.

**Windows.** The 1981 window is November 1978 to June 1983, split at January 1981, as in the earlier work.
This is cycle month 32-87 of Cycle 21, split at cycle month 58. We use the same cycle months for Cycles 22
(1989-05 to 1993-12), 23 (1999-04 to 2003-11) and 24 (2011-08 to 2016-03). We also repeat the
monthly-mean model of the earlier campaign work without source effects
(`files/results/monthly_1981_effects.csv`).

**Decomposition.** We write the change of the Locarno Wolf count as a group term s·ΔlogLG plus a spot term
(1−s)·ΔlogLW. Here s = 0.48 is the pre-1981 share of 10·LG in LR. We then replace the Locarno changes with
the DPD changes in G and N.

## Results

All values are post/pre factors at matched F10.7 with flat levels, on 1,357 common days of SN, DPD and
Locarno (180-day blocks), unless the text gives a different variant. Full tables are in `files/results/`.

### 1. Across January 1981, groups fall, but spots and spot area do not (Figure 1)

| Count | Flat, F10.7 | Separate slopes, F10.7 | Flat, Mg II |
|---|---|---|---|
| SILSO SN | 0.873 (0.83-0.92) | 0.852 (0.77-0.95) | 0.883 (0.84-0.94) |
| Locarno Wolf count LR | 0.855 (0.81-0.91) | 0.811 (0.73-0.91) | 0.864 (0.82-0.92) |
| DPD groups G | 0.884 (0.84-0.93) | 0.859 (0.77-0.95) | 0.886 (0.83-0.94) |
| DPD clusters, 10° | 0.841 (0.78-0.91) | 0.901 (0.80-1.02) | 0.844 (0.78-0.91) |
| DPD clusters, 6° | 0.876 (0.81-0.95) | 0.873 (0.76-0.99) | 0.871 (0.80-0.94) |
| DPD clusters, 2.5° | 1.015 (0.94-1.10) | 0.918 (0.79-1.06) | 1.015 (0.94-1.09) |
| DPD spots N | 1.014 (0.89-1.16) | 0.846 (0.70-1.01) | 1.046 (0.94-1.18) |
| DPD spot area A | 1.060 (0.92-1.23) | 0.947 (0.80-1.10) | 1.094 (0.98-1.23) |
| Share of spots ≤2 MSH | 0.993 (0.94-1.05) | 1.090 (0.99-1.20) | 1.001 (0.95-1.05) |
| DPD area per group A/G | 1.199 (1.04-1.39) | 1.102 (0.92-1.33) | 1.234 (1.11-1.37) |
| **SN / DPD groups** | **0.987 (0.93-1.05)** | **0.992 (0.88-1.12)** | **0.997 (0.94-1.06)** |

- SN falls by the same fraction as the DPD group count. SN/G stays at 0.973-1.035 in all twelve variants
  (two references × two time models × three samples: all Locarno observers, Cortesi only, DPD days
  without the Locarno requirement). The Cortesi-only value is 1.005 (0.96-1.05). Year by year, SN/G is 1.03
  and 0.99 in 1979 and 1980, and 0.99 and 1.04 in 1981 and 1982 (`cycle_year_factors.csv`).
- The fall also occurs in position clusters at group scale (6° and 10°). It does not occur at the 2.5°
  scale of spot fragments. Thus the change is not only a change of NOAA or observer grouping practice.
  The same spots lie in fewer clusters.
- With flat levels, the DPD spot count and spot area do not fall. The spot-size distribution does not
  change: the share of the smallest spots is 0.993 (0.94-1.05). Thus we find no small-spot deficit and no
  general decrease of spot size. Area per group increases by about 20%. With separate time slopes, the DPD
  spot count also falls (0.846, 0.70-1.01). Thus the spot-count result depends on the time model, but the
  group and cluster results do not.
- The monthly-mean model of the earlier work, without source effects, gives the same pattern:
  SN 0.868, G 0.890, N 1.012, A 1.060 (Gyula days only: G 0.865, N 0.957, A 1.060).

### 2. Decomposition of the Wolf count (Figure 4 in files/figures)

With flat levels, the Locarno fall has a group term of −7.6% and a spot term of −8.0% (log ×100).
The DPD group term is −5.9% (−8.5 to −3.3), and the DPD spot term is +0.7% (−6.1 to +7.7). Thus DPD
changes alone give a Wolf-count factor of 0.949 (0.88-1.03). This leaves 0.919 (0.85-0.99) of the SN change
unexplained. That part is the Locarno weighted spot count per DPD spot, LW/N = 0.846 (0.74-0.96); for
Cortesi only it is 0.890 (0.80-0.99). With separate slopes, the DPD changes explain all of the SN change
(DPD counterfactual 0.852; remainder 1.000, 0.87-1.14). Thus about half of the 1981 SN fall is a group-count
fall that independent catalogues share. Whether the other half is a station counting change or a real
spot-count change depends on the time model.

### 3. Group counts also fall in the same phase of later cycles (Figure 2)

| Count, flat, F10.7 | C21 (1981) | C22 (1991-07) | C23 (2001-06) | C24 (2013-10) |
|---|---|---|---|---|
| SILSO SN | 0.873 (0.83-0.92) | 1.032 (0.98-1.08) | 0.979 (0.92-1.04) | 0.882 (0.79-1.00) |
| DPD groups G | 0.884 (0.84-0.93) | 0.940 (0.86-1.02) | 0.887 (0.83-0.95) | 0.965 (0.88-1.07) |
| DPD clusters, 6° | 0.876 (0.81-0.95) | 0.872 (0.80-0.96) | 0.910 (0.83-1.00) | 1.026 (0.95-1.12) |
| DPD spot area A | 1.060 (0.92-1.23) | 1.103 (0.97-1.24) | 1.108 (0.97-1.27) | 0.909 (0.79-1.03) |
| SN / DPD groups | 0.987 (0.93-1.05) | 1.097 (1.00-1.20) | 1.104 (1.02-1.19) | 0.913 (0.83-1.00) |

The group and cluster falls at matched F10.7 recur in Cycles 22 and 23. In Cycle 23 the DPD group fall
(0.887) is equal to the 1981 value. Against the mean of Cycles 22-24, the Cycle 21 change is 0.950
(0.88-1.02) for DPD groups and 0.938 (0.85-1.03) for 6° clusters. For SN it is 0.907 (0.84-0.98). Thus
the SN fall in 1981 is larger than the SN change at the same phase in later cycles. But the SN/G ratio
varies from 0.91 to 1.10 between cycles at this phase, and Cycle 24 SN (0.882) is as low as Cycle 21.
These cross-cycle intervals include only within-window noise, not the spread between cycles. Thus the data
do not show that the 1981 change of SN relative to groups is unusual.

### 4. Cross-cycle levels are not interpretable with DPD

At matched F10.7, DPD spot counts per unit emission in Cycles 21-23 are 0.64-0.74 times the Cycle 24 value,
and the smallest-spot class is 0.51-0.60 times (`cycle_year_factors.csv`). In Cycle 24 most DPD days come
from Kanzelhöhe CCD images, and DPD changed its measurement method in 1988. We think that these source and
method changes cause most of the level differences. Thus we do not use DPD to test the long-term decline
of SN relative to emission across cycles.

## Interpretation

The 1981 fall of SN relative to F10.7 and Mg II is not a loss of small spots and not a decrease of spot
size in the DPD. Under the main model, the same number of spots and the same spot area occur in about 12%
fewer groups and fewer group-scale position clusters. The Wolf formula gives each group a weight of 10, so
a more concentrated arrangement of the same spots decreases SN while area-related emission stays the same.
Three independent group assignments (DPD/NOAA, Locarno, and Kislovodsk in 5250d28f) and an
observer-independent clustering rule agree. Similar falls occur at the same phase in Cycles 22 and 23. Thus
we consider that at least half of the 1981 fall is a solar change in how spots are grouped, and probably a
recurrent change of the declining phase. It is probably not a calibration step of the index. This result
supports the earlier phase-control results of 73bfd229, which found SN falls of 12.8% and 14.1% at the same
phase of Cycles 21 and 20. For long sunspot-based records, it means that SN per unit emission depends on how
concentrated the spots are, and not only on how many spots there are or how large they are.

## Limitations

- **Possible DPD changes.** DPD 1979-1984 is marked preliminary. DPD group numbers start from NOAA numbers.
  The position clusters use DPD spot positions, which have a precision of about 0.1°. A shared change in the
  measurement or identification of spots at Gyula after 1980 could hide a real spot-count fall. We have no
  third per-spot catalogue for 1978-1983 to test this.
- **Time model.** With separate time slopes, DPD spot counts fall by about 15%. Then all of the SN change
  agrees with the DPD changes. The group, cluster and SN/G results do not depend on the time model; the
  spot-count result does.
- **Emission matching.** The model matches emission on the same day. It does not include memory
  (c6d62719) or spectral changes. The F10.7 and Mg II references agree. Matched emission is not the same as
  matched magnetic flux.
- **Few cycles.** Only four same-phase windows are available. The cross-cycle contrasts include only
  within-window noise, so they overstate certainty about a recurrent pattern. Source mixtures differ by
  cycle: the Gyula/Debrecen shares change near the split dates of Cycles 22-23, and Kanzelhöhe dominates Cycle 24. Source fixed
  effects remove only constant source differences.
- **Locarno observers.** Observer 5 stops at the end of 1980. The Cortesi-only sample gives a smaller
  Locarno spot-count fall relative to DPD (LW/N 0.890), so part of the Locarno spot term can come from the
  observer change.
- **Clustering rule.** Single linkage with fixed distances is a simple rule, not a magnetic definition of
  an active region.
- **Cause.** We do not identify the physical cause of the concentration. Candidates are activity nests and
  complexes of the declining phase. The study gives no correction for the sunspot record.

## Figures

- `files/figures/fig1_1981_factors.png`: post/pre factors across January 1981 for each count type.
- `files/figures/fig2_phase_cycles.png`: the same phase window in Cycles 21-24.
- `files/figures/fig3_quarterly_ratio.png`: quarterly observed/predicted ratios. The display fit is a power
  law in F10.7 with source effects, fitted on November 1978 to December 1980 only. It is not the test model.
- `files/figures/fig4_decomposition.png`: group and spot terms of the Wolf-count change.

## Files

- `files/code/01_parse_dpd.py`: parses DPD files into daily counts, area and size classes (scratch).
- `files/code/05_clusters.py`: position clusters at 2.5°, 4°, 6° and 10° (scratch).
- `files/code/02_analysis.py`: monthly-mean model of the earlier work (`monthly_1981_effects.csv`,
  `size_decomposition.csv`, `origin_days_by_year.csv`, `inputs.json`).
- `files/code/03_daily_phase.py`: main daily models, cycle windows, contrasts and decomposition
  (`daily_phase_effects.csv`, `cycle21_contrasts.csv`, `wolf_decomposition.csv`).
- `files/code/04_cycle_levels.py`: cycle and year factors (`cycle_year_factors.csv`).
- `files/code/06_figures.py`: figures.
- `files/results/environment.json`: software versions. `files/EXTERNAL_DATA.md`: sources and terms.

Columns of `daily_phase_effects.csv`: reference (F = F10.7, M = Mg II), sample (joint = all Locarno
observers; cortesi; dpd = DPD and SN days without the Locarno requirement), trend, block (bootstrap block
length in days), cycle, component, factor, low, high, days, dispersion (square root of the quasi-Poisson
scale), origins (source fixed effects), window and split. Component names: SN; DPD G, N, Npen (spots with
their own penumbra), Nshared (umbrae in a shared penumbra), Nc (spots within 0.7 radius), A, U (umbral
area), Gu/G0 (groups with/without measured umbra), a0_2 ... a100p (size classes), K2.5 ... K10 (clusters),
K4_big (4° clusters with at least 10 MSH); Locarno LG, LW, LR; and ratios such as SN/G.

## Reproduction

1. `bash files/code/retrieve_inputs.sh SCRATCH` downloads all inputs into a folder outside the publication.
   Compare the SHA-256 values with `files/results/inputs.json`.
2. `bash files/code/run_all.sh SCRATCH/datasets SCRATCH/work` runs all steps (about 6 minutes on one CPU,
   Python 3.12 with numpy, pandas, scipy, statsmodels, patsy and matplotlib; versions in `environment.json`).
   Outputs go to `SCRATCH/work/out`. A fresh rerun on the campaign machine gave byte-identical result tables.

## References

- Baranyi, Győri and Ludmány (2016), Solar Physics 291, 3081, doi:10.1007/s11207-016-0930-1 (DPD).
- Győri, Ludmány and Baranyi (2017), MNRAS 465, 1259, doi:10.1093/mnras/stw2667 (DPD).
- Lefèvre and Clette (2011), A&A 536, L11, doi:10.1051/0004-6361/201118034 (small-spot deficit in Cycle 23 from DPD).
- Clette (2021), J. Space Weather Space Clim., doi:10.1051/swsc/2020071 (F10.7-SN relation and 1981 jump).
- Mursula et al. (2024), A&A, doi:10.1051/0004-6361/202449231 (long-term change in emission per spot).
- Snow et al. (2014), doi:10.1051/swsc/2014001 (Mg II composite); SILSO doi:10.24414/qnza-ac80; Locarno doi:10.5281/zenodo.19118343.
- Campaign publications cited in sci.json.
