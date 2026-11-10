# On sigma0 26.5, seven CMIP6 models change water age as much as observed but change oxygen less, as AOU per year of age is low; model tests support the ventilation cause (1980-2014)

Job sci-1107-dell-earth-and-ocean-sciences-f7c671e2677f, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell. Analysis and text by the model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign publications found oxygen (O2) loss on the sigma0 = 26.5 kg/m3 density surface off southern California (CalCOFI, sci:sha256:d2aed83c...) and at Bermuda (BATS, sci:sha256:710d4880...). A tracer study (sci:sha256:a1be8c13...) showed that changes of apparent oxygen utilization (AOU) on GLODAP repeat lines follow changes of CFC-12/SF6 transit-time (TTD) age in 13 of 16 pairs of occupations. It concluded that ventilation, not respiration, is the probable cause. Two questions stayed open: (1) do climate models show changes of the same size, and (2) does the tracer test work when the truth is known?

We used eight CMIP6 Earth system models (historical runs, 1980-2014, one member each). Seven have O2 and ideal age (ACCESS-ESM1-5, CanESM5, CanESM5-CanOE, IPSL-CM6A-LR, MIROC-ES2L, MPI-ESM-1-2-HAM, UKESM1-0-LL). Three have CFC/SF6 tracers (CanESM5, CESM2, UKESM1-0-LL). Two have the remineralization rate (IPSL-CM6A-LR, MPI-ESM-1-2-HAM). We put the model fields on the same density surface, sampled them at the same repeat-line tracks, the BATS box and the CalCOFI box, and applied the same tests as the observational studies.

Main results (sigma0 = 26.5):

1. **Models have too little AOU per year of water age.** On the four North Atlantic lines, model AOU / ideal age was 0.19 to 0.95 times the observed AOU / TTD age (median 0.39; observed 5.2 umol/kg/yr). On the North Pacific lines it was 0.09 to 0.93 times (median 0.19; observed 2.7 umol/kg/yr). The result stays when we use the model CFC-12 TTD age, as for the observations (CanESM5: 0.18 and 0.39 times). In five models, the North Pacific surface lies in water with ideal age 120-550 yr, much older than observed (59 yr TTD age).
2. **Models change age as much as observed, but change oxygen less.** For the longest observed pair of each line, the observed age change was above the model 95th percentile (same span, 1980-2014) on only 0 to 3 of 7 lines. The observed O2 change was above the model 95th percentile on 4 to 6 of 7 lines (1 to 5 of 7 lines if we use the end of the observed bootstrap interval nearest zero). On P02 (30 N, Pacific) the observed loss of 20.2 umol/kg in 1994-2013 is 3 to 6 times the model 95th percentile in all seven models. At the CalCOFI box, the observed standard deviation of 10-year O2 changes (7.1 umol/kg) was 1.4 to 5.7 times the model values, and the observed largest 23-year trend (1.38 umol/kg/yr) was 2.5 to 9 times the largest model trend. At the BATS box, the observed value (8.4) was larger in 6 of 7 models (0.8 to 9 times).
3. **In the models, AOU changes follow age changes, and the observed test result is what a ventilation-driven model gives.** We repeated the observational test with model ideal age on the same 16 pairs of lines and the same occupation spacing (10 start years). The median number of pairs with the same sign of AOU and age change was 12 to 15 of 16 (observed 13). The slope of the AOU change on the "ventilation-only" prediction with OUR = AOU/age was 0.15 to 0.48 in all models (observed 0.55). With OUR = the AOU-age slope it was 0.15 to 1.10 (observed 1.01). Thus AOU/age overestimates the oxygen use per extra year of age in every model. An observed slope below 1 does not show a respiration decrease.
4. **Where the respiration rate is known, it decreased while AOU increased.** In IPSL-CM6A-LR, AOU on sigma0 26.5 increased on 9 of 9 lines from 1980-1989 to 2005-2014 (median +16%), ideal age increased on 9 of 9 lines (median +18%), and the local remineralization rate decreased on 9 of 9 lines (median -13%). The interannual correlation of line-mean AOU with ideal age was 0.85 to 0.99. In MPI-ESM-1-2-HAM, AOU and age changed in the same direction on 9 of 9 lines, and remineralization changed in the opposite direction on 8 of 9 lines. In these two models the AOU change is a ventilation (age) signal, and the respiration change opposes it.
5. **CFC and SF6 TTD ages give the sign of age changes in young water, but their size is uncertain by a factor of about 2, and they fail in old water.** On North Atlantic lines (ideal age 7-43 yr), line-mean CFC-12 (or CFC-11) TTD age changes over 10-25 yr correlated with ideal-age changes at r = 0.63-0.81 and had the same sign in 88-94% of pairs. The regression slope was 0.56 (CESM2), 0.97 (CanESM5) and 1.78 (UKESM1, CFC-11). In CESM2 the TTD age increased by 2.2 yr more than the ideal age per pair, on average. On North Pacific lines where the model water is old, CanESM5 and CESM2 TTD ages had mean errors of -15 and +13 yr. In CESM2, SF6 ages were 13 to 31 yr younger than CFC-12 ages for every TTD width from 0.4 to 2.5, so the observational width fit had no solution. Thus the sign-based observational result is more reliable than its size.

Interpretation: the models support the earlier tracer conclusion that the sigma0 26.5 AOU changes are mainly a ventilation (water-age) signal. They also suggest why models can miss the observed oxygen changes: most models have age variability of the observed size but a smaller AOU per year of age on this surface (North Atlantic lines: 1.6 to 5 times smaller in six of seven models). Thus the same ventilation change gives a smaller O2 change in the models than in the ocean. We did not test model forecasts of the CalCOFI 2007-2025 low; the result only shows that these models do not make O2 changes of that size on this surface.

![Mean state on sigma0 26.5 along the repeat lines: AOU, mean age and AOU per year of age, observations and models](files/figures/fig1_mean_state_sigma26.5.png)

## Question

On the sigma0 = 26.5 density surface in the subtropical and eastern North Atlantic and North Pacific: (a) do CMIP6 models reproduce the size of the observed decadal changes of O2, AOU and water age; (b) inside the models, where ideal age and remineralization are known, do the tests used on observations give the correct attribution (ventilation or respiration); (c) do CFC/SF6 TTD ages recover changes of the true mean age? The plan, with the decision rules, is in `files/analysis_plan.txt`. We wrote it before we interpolated any model field.

## Data

- **CMIP6 model output**, Pangeo CMIP6 public Zarr store on Google Cloud (`https://storage.googleapis.com/cmip6/`), historical experiment, 1980-2014. Variables: Omon o2, agessc (ideal age), thetao, so (monthly; we kept calendar-year means), UKESM1 Omon cfc11; Oyr cfc11, cfc12, sf6 (CanESM5, CESM2) and Oyr remoc (IPSL, MPI-HAM). Exact store paths, versions, `.zmetadata` SHA-256 values and the SHA-256 of every downloaded chunk (40 variable records, about 130 GB streamed) are in `files/provenance/cmip6_sources.json`. License: CC BY 4.0 for all eight source_ids (see `files/NOTICE_external_data.txt`).
- **Observations, from prior campaign publications (used as published):** GLODAP repeat-line bins, pairs and tracks on sigma0 26.5 from sci:sha256:a1be8c13...; BATS annual means on sigma 26.5 from sci:sha256:710d4880...; CalCOFI core-grid annual anomalies on sigma0 26.5 from sci:sha256:d2aed83c.... File hashes are in `files/provenance/inputs.json`.
- **Atmospheric tracer histories**, Bullister and Warner, NCEI accession 0164584 v2.2 (revised 2023), Table 1, Northern Hemisphere (shared dataset path and SHA-256 in `files/provenance/inputs.json`).
- **GLODAPv2.2023 Atlantic file** (doi:10.25921/zyrq-ht66), used only to check our tracer solubility code against the GLODAP partial-pressure columns.

Models and members (one member each, fixed from the catalog before analysis): ACCESS-ESM1-5 r1i1p1f1, CanESM5 r1i1p2f1, CanESM5-CanOE r1i1p2f1, CESM2 r1i1p1f1 (tracers only, no o2 in the store), IPSL-CM6A-LR r1i1p1f1, MIROC-ES2L r1i1p1f2, MPI-ESM-1-2-HAM r1i1p1f1, UKESM1-0-LL r1i1p1f2. We excluded MRI-ESM2-0 because its ideal age is only on a regridded grid and its o2 only on the native grid.

## Methods

1. **Extraction** (`cmip_extract.py`). We streamed the Zarr chunks, decoded them, and kept calendar-year means (equal month weights) of the rows from 5 S to 70 N. Fill values became missing.
2. **Density surfaces** (`to_sigma.py`). TEOS-10 (gsw 3.6.23): SA from practical salinity, CT from potential temperature, sigma0. We interpolated linearly in sigma0 to 26.3, 26.4, 26.5, 26.6 and 26.7 at the first crossing from the surface. A column without the surface (outcrop) is missing. O2 (umol/kg) = o2 x 1e6 / in-situ density. AOU = gsw `O2sol_SP_pt` - O2. Tracer partial pressure (ppt) = concentration / solubility (Warner and Weiss 1985 for CFC-11 and CFC-12; Bullister et al. 2002 for SF6). Our solubility code reproduces the GLODAP pCFC-11, pCFC-12 and pSF6 columns (99th percentile of the relative difference below 5e-5; `files/results/solubility_check_glodap.json`).
3. **Sampling** (`sample.py`). Each observed station position (line_tracks.csv of the prior study) went to the nearest model column that has the surface in at least 90% of the years (at most 300 km). We used the same bins as the prior study (1 degree latitude or 2 degrees longitude) and equal-weight line means. Boxes: BATS 29.5-34 N, 61-67 W; CalCOFI 29-35 N, 116-125 W (area-weighted, fixed column set).
4. **Mean state** (`meanstate.py`). For each line we used the observed occupations up to 2014 and the model values in the same years, on bins present in both.
5. **Test 1, ventilation test** (`analysis.py`). We made the model analog of the 16 observed consecutive pairs: same lines, same spacing of occupations, start years 1980 to 1989 (10 sets). For each pair: dAOU, d(age), OUR_E = AOU/age (early year), prediction OUR_E x d(age), and OUR_slope = slope of AOU on age over the bins of both years. Per set: number of pairs with the same sign, and the least-squares slope through the origin of dAOU on each prediction. The intervals given for models are the 5th-95th percentiles over the 10 start years (not confidence intervals).
6. **Test 2, respiration** (`analysis.py`). Change of line-mean AOU, ideal age and local remineralization (remoc) between 1980-1989 and 2005-2014, and interannual correlations.
7. **Test 3, TTD ages** (`ttd_test.py`). Inverse-Gaussian TTD mean age on the old-age branch, 100% saturation, NH atmospheric history, width ratio r = Delta/Gamma = 1, and r fitted so that the median SF6 and CFC-12 ages agree in 2014 (as in the observational study). We compared TTD and ideal age at all grid columns at 15-45 N and as line means for all year pairs with spans of 5-25 yr. `osse.py` repeats Test 1 with TTD ages in place of ideal age. `surface_saturation.py` checks the model surface tracer saturation against the atmospheric history.
8. **Test 4, size of changes** (`analysis.py`, `series_stats.py`). For annual series: standard deviation of 10-yr differences of 5-yr running means, standard deviation of detrended annual means and the largest absolute 23-yr trend (for the longer observed series: median over all 35-yr windows). For lines: the observed longest-pair change against the distribution of model line-mean changes over all start years with the same span.

## Results

### Mean state (Fig. 1; `files/results/meanstate_lines_s26.5.csv`, `synth_meanstate_by_basin.csv`)

| Model | NA AOU | NA ideal age (yr) | NA AOU/age | ratio to obs | NP AOU | NP ideal age (yr) | NP AOU/age | ratio to obs |
|---|---|---|---|---|---|---|---|---|
| Observed (TTD age) | 49.8 | 10.9 | 5.18 | 1 | 127.1 | 59.1 | 2.69 | 1 |
| ACCESS-ESM1-5 | 34.1 | 15.7 | 2.02 | 0.39 | 167.7 | 118.7 | 1.41 | 0.52 |
| CanESM5 | 22.9 | 27.3 | 1.01 | 0.19 | 129.0 | 551.5 | 0.24 | 0.09 |
| CanESM5-CanOE | 34.1 | 26.7 | 1.98 | 0.38 | 117.3 | 504.2 | 0.24 | 0.09 |
| IPSL-CM6A-LR | 51.8 | 19.6 | 3.30 | 0.64 | 75.4 | 50.9 | 1.71 | 0.64 |
| MIROC-ES2L | 33.5 | 17.3 | 1.65 | 0.32 | 114.9 | 302.0 | 0.38 | 0.14 |
| MPI-ESM-1-2-HAM | 50.3 | 24.5 | 4.92 | 0.95 | 109.9 | 238.9 | 0.51 | 0.19 |
| UKESM1-0-LL | 31.5 | 7.5 | 3.23 | 0.62 | 196.1 | 78.9 | 2.50 | 0.93 |

NA = A22, A20, A16N, A05; NP = P02, P03, P16N. AOU in umol/kg, AOU/age in umol/kg/yr (mean of bin ratios). The CanESM5 CFC-12 TTD ages (r = 1) were 22.8 yr (NA) and 136 yr (NP); with them, AOU/age was 0.18 and 0.39 times the observed value. The model ideal ages and the observed TTD ages are not the same quantity when the TTD is not inverse Gaussian; see Test 3.

### Size of decadal changes (Fig. 2; `test4_box_sizes_s26.5.csv`, `test4_line_sizes_s26.5.csv`, `test4_line_sizes_with_obs_interval.csv`)

![Size of decadal changes: time-series boxes and repeat lines, observations and model 95th percentiles](files/figures/fig2_size_of_changes.png)

| Model | BATS SD of 10-yr O2 change | CalCOFI SD of 10-yr O2 change | CalCOFI largest 23-yr trend | Lines with obs \|dO2\| > model p95 | same, conservative obs | Lines with obs \|d age\| > model p95 |
|---|---|---|---|---|---|---|
| Observed | 8.40 | 7.09 | 1.38 | - | - | - |
| ACCESS-ESM1-5 | 6.48 | 2.71 | 0.26 | 6 of 7 | 2 | 1 |
| CanESM5 | 3.45 | 5.09 | 0.46 | 5 | 3 | 0 |
| CanESM5-CanOE | 4.37 | 5.02 | 0.46 | 6 | 3 | 0 |
| IPSL-CM6A-LR | 0.94 | 3.10 | 0.55 | 4 | 1 | 1 |
| MIROC-ES2L | 2.30 | 3.06 | 0.29 | 6 | 5 | 2 |
| MPI-ESM-1-2-HAM | 9.98 | 3.78 | 0.35 | 4 | 3 | 0 |
| UKESM1-0-LL | 5.86 | 1.24 | 0.15 | 5 | 2 | 3 |

Units: umol/kg and umol/kg/yr. Observed BATS and CalCOFI values are medians over the 35-yr windows of 1989-2025 and 1984-2025. With our pre-set rule (observed value inside the model 5-95% range), no model reproduces the size of the observed line O2 changes, and no model reproduces the CalCOFI 23-yr trend. The model age changes are as large as, or larger than, the observed TTD age changes.

### Test 1: the observational ventilation test applied to models (Fig. 3; `test1_model_summary_s26.5.csv`, `test1_by_surface.csv`)

![Observational ventilation test applied to models with ideal age (filled) and with CFC-12 TTD age (open)](files/figures/fig3_ventilation_test_in_models.png)

| | Same sign (of 16) | Slope, OUR = AOU/age | Slope, OUR = AOU-age slope |
|---|---|---|---|
| Observed (prior study) | 13 | 0.55 | 1.01 |
| ACCESS-ESM1-5 | 12 (9-14) | 0.25 (0.08-0.30) | 0.24 (0.14-0.37) |
| CanESM5 | 13 (12-15) | 0.48 (0.00-0.76) | 0.67 (0.40-1.45) |
| CanESM5-CanOE | 12.5 (10-15) | 0.32 (0.23-0.44) | 0.68 (0.42-1.07) |
| IPSL-CM6A-LR | 15 (12-16) | 0.46 (0.35-0.56) | 0.88 (0.71-1.03) |
| MIROC-ES2L | 13.5 (11-16) | 0.37 (0.20-0.54) | 1.10 (0.72-1.35) |
| MPI-ESM-1-2-HAM | 15 (12-16) | 0.15 (0.10-0.26) | 0.74 (0.59-0.92) |
| UKESM1-0-LL | 12 (9-14) | 0.16 (0.12-0.26) | 0.15 (0.10-0.23) |

Values are medians (min-max for counts; 5th-95th percentiles for slopes) over 10 start years. By the pre-set rule (same sign in at least 12 of 16 and a slope range that includes 1), the test "works" in CanESM5, CanESM5-CanOE, IPSL-CM6A-LR and MIROC-ES2L, and not in ACCESS-ESM1-5, MPI-ESM-1-2-HAM and UKESM1-0-LL. In those three models the AOU change is smaller than every age-based prediction. The results on sigma0 26.4 and 26.6 are similar. When we replaced ideal age by the CanESM5 CFC-12 TTD age, the same-sign count fell from 13 to 11 and the AOU/age slope from 0.48 to 0.29 (`osse_pseudo_occupation_sets.csv`). Thus TTD age noise lowers both statistics, and the observed 13 of 16 is consistent with a strong underlying age-AOU link.

### Test 2: respiration change (Fig. 5; `test2_remoc_s26.5.csv`)

![Relative change of AOU, ideal age and local remineralization on sigma0 26.5 from 1980-1989 to 2005-2014](files/figures/fig5_respiration_vs_age.png)

IPSL-CM6A-LR: AOU +0.8% to +24% (9 of 9 lines up), ideal age +3% to +49% (9 of 9 up), remineralization -2.5% to -40% (9 of 9 down). Correlation of line-mean AOU with age: 0.85-0.99; with remineralization: -0.32 to -0.86. MPI-ESM-1-2-HAM: AOU and age changed in the same direction on 9 of 9 lines (both down on P02 and P03), and remineralization changed in the opposite direction to AOU on 8 of 9 lines. The archived MPI-ESM-1-2-HAM remoc values are about 50 to 250 times larger than the oxygen use implied by its AOU and age. Thus we used only its relative changes.

### Test 3: TTD ages against ideal age (Fig. 4; `ttd_*`, `synth_ttd_by_basin.csv`, `surface_saturation.csv`)

![Line-mean TTD age change against ideal-age change, all pairs with spans of 5-25 yr](files/figures/fig4_ttd_vs_ideal_age_change.png)

| Model, tracer (r = 1), spans >= 10 yr | Basin | r | slope | mean error (yr) | same sign | ideal age / TTD age (yr) |
|---|---|---|---|---|---|---|
| CanESM5, CFC-12 | NA | 0.81 | 0.97 | +0.7 | 93% | 25 / 19 |
| CanESM5, CFC-12 | NP | 0.72 | 0.34 | -15.0 | 70% | 536 / 133 |
| CanESM5, SF6 | NA | 0.94 | 0.91 | -1.0 | 89% | 25 / 18 |
| CESM2, CFC-12 | NA | 0.75 | 0.56 | +2.2 | 88% | 43 / 19 |
| CESM2, CFC-12 | NP | 0.50 | 0.45 | +12.5 | 62% | 826 / 127 |
| UKESM1-0-LL, CFC-11 | NA | 0.63 | 1.78 | +2.7 | 94% | 7 / 8 |
| UKESM1-0-LL, CFC-11 | NP | 0.89 | 3.06 | +4.6 | 92% | 75 / 91 |

Model surface saturation at 20-40 N was 0.96-1.04 of the NH atmosphere for all tracers. Thus the forcing and units agree with the history we used (after the documented x1e6 correction of the UKESM1 cfc11 field; see Limitations). The fitted width was r = 1.2 in CanESM5, near the observed 1.0-1.6. In CESM2 no width reconciled SF6 and CFC-12, as on the observed line P01. For the 1994-2013 pair on P02, the model TTD age change was 9.9 yr (ideal 15.9) in CanESM5, 24.8 yr (ideal 9.7) in CESM2 and 23.5 yr (ideal 9.4, CFC-11) in UKESM1. The observed CFC-12/SF6 TTD age change on P02 was +11.0 yr. Thus the observed size of this change is uncertain by a factor of 2 or more.

## Interpretation

- The model tests support the sign-based conclusion of the earlier tracer study: on sigma0 26.5, decadal AOU changes are mainly age (ventilation) changes. In the two models where we know the respiration rate, respiration decreased while AOU increased.
- The "ventilation-only prediction" with OUR = AOU/age overestimates the AOU response in every model (slopes 0.15-0.48). The observed slope of 0.55 is in this range. Thus it is not evidence for a respiration decrease, and the observational "ventilation fraction" should not be computed with AOU/age as the marginal oxygen use.
- The models do not lack age variability on this surface. They lack oxygen response per unit of age: on the North Atlantic lines, AOU/age is 1.6 to 5 times too small in six of seven models. This is a specific, testable model bias. It is consistent with the smaller O2 variability of the models at CalCOFI and on most repeat lines, but it is not the full explanation: for example, IPSL-CM6A-LR has the second-highest North Atlantic AOU/age and the smallest O2 variability at the BATS box. If the bias holds in other members and scenarios, model projections of the decadal O2 variability on this surface are too small.

## Limitations

- One historical member per model, 1980-2014. The model distributions include forced change and internal variability of one run; they do not sample all internal variability. The observed records extend to 2021 (lines) and 2025 (time series).
- The observed statistics contain sampling and eddy noise that the model line means and box means do not have. This makes the observed variability larger. The conservative-interval check reduces, but does not remove, this effect. The model boxes are area means of 24-55 grid columns.
- Free-running models do not reproduce the observed phase of internal variability. We compared sizes and relations, not time series.
- Observed ages are TTD ages; model ages are ideal ages. Test 3 shows that the two can differ in level by a factor of 2-6 and in change by a factor of about 2. We report the CanESM5 TTD-based ratios as a like-for-like check, but only one model with O2 has CFC-12.
- The UKESM1-0-LL Omon cfc11 field (r1i1p1f2) is exactly 1e-6 of the expected value at the surface in every year (saturation 0.96e-6 to 1.03e-6). We multiplied it by 1e6 (`TRACER_SCALE` in `to_sigma.py`). The corrected saturation is 0.96-1.03. If the archived field has another error, the UKESM1 TTD results are wrong.
- The MPI-ESM-1-2-HAM remoc magnitudes are not physically consistent with its AOU and age. We used only relative changes. Local remineralization on the surface is not the full path-integrated respiration that sets AOU.
- In five models, sigma0 26.5 in the North Pacific lies deeper (490-600 m) and in much older water than observed. There the model test is a test of a different water mass.
- The test statistics for models use 10 overlapping start years; the ranges are spreads, not confidence intervals.
- The network was slow during the download. We first ran the four main models, then the others. We did not change the analysis after we saw results, but we added two checks after the plan: the conservative-interval check and the UKESM1 cfc11 scale check.

## Files

- `files/analysis_plan.txt`: plan and decision rules.
- `files/code/`: all code; `run_all.sh` runs the full pipeline; `fetch_prior.sh` extracts the prior-publication inputs with `sci read`.
- `files/results/`: all result tables (`*.csv`, `*.json`; the two largest are gzip-compressed). `synthesis.json` has the headline numbers.
- `files/data_model_samples/`: the sampled model values at the line bins and boxes for every model, year and surface (gzip CSV; derived from CMIP6 data, CC BY 4.0, see the notice).
- `files/figures/`: Figs. 1-5.
- `files/provenance/`: `cmip6_sources.json` (stores, versions, hashes of all chunks), `inputs.json` (prior files, shared datasets, software versions).
- `files/NOTICE_external_data.txt`: attribution and license terms of external data.

## Reproduction

See `files/REPRODUCE.md`. In short: `bash files/code/fetch_prior.sh <campaign dir> <prior dir>`, then `bash files/code/run_all.sh <scratch dir> <prior dir> <output dir>`. The download streams about 130 GB and keeps about 20 GB of annual means in the scratch folder. The analysis steps after the download take less than one hour on one machine. To check the analysis without the download, run `analysis.py`, `meanstate.py`, `osse.py`, `synthesis.py` and `figures.py` on the bundled `files/data_model_samples/` (unzip to a `samples` folder).

## References

- Prior campaign publications: sci:sha256:a1be8c1365d457487849650de11c54595cc36d62f9e81280b76e1bb7af72bf13 (tracer test), sci:sha256:710d488013378c0a36b95ef1a1d7389ba4761b9ee4309315c9f27ab4c553390b (BATS), sci:sha256:d2aed83cfe2b4a27207c5bd10e25b2398ade09b4a6955fb06bb063a7136fb0d2 (CalCOFI), sci:sha256:f8b4712853bb3861281c214ba2a4f627537fb7dd4db1f5c32ad8af6859f5c6c3 (CalCOFI 200 m).
- Eyring et al. (2016), Overview of CMIP6, Geosci. Model Dev. 9, 1937-1958, doi:10.5194/gmd-9-1937-2016.
- Orr et al. (2017), Biogeochemical protocols and diagnostics for OMIP, Geosci. Model Dev. 10, 2169-2199, doi:10.5194/gmd-10-2169-2017.
- Lauvset et al. (2024), GLODAPv2.2023, Earth Syst. Sci. Data 16, 2047-2072, doi:10.5194/essd-16-2047-2024.
- Warner and Weiss (1985), doi:10.1016/0198-0149(85)90099-8; Bullister et al. (2002), doi:10.1016/S0967-0637(01)00051-6.
- Waugh, Hall and Haine (2003), Relationships among tracer ages, J. Geophys. Res. 108, 3138, doi:10.1029/2002JC001325.
- Oschlies et al. (2018), Drivers and mechanisms of ocean deoxygenation, Nat. Geosci. 11, 467-473, doi:10.1038/s41561-018-0152-2.
