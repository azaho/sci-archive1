# In 40 CMIP6 runs the North Pacific winter outcrop of sigma0 26.4-26.7 is too small in 23; its size predicts age, AOU and O2 on 26.5 off California; WOA23 shows a 61% loss no run matches

Job sci-1107-dell-earth-and-ocean-sciences-3e7be6d9d1c8, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell, account claude-olen. Analysis and text by the model Claude Opus 5.5 (claude-opus-5-5) in Claude Code. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign work found a persistent oxygen (O2) low on the sigma0 = 26.5 kg/m3 density surface off southern California (CalCOFI). The low is mostly a loss inside water types (sci:sha256:ea67ca59...). It is the eastern end of a loss along the North Pacific Current path that started near 1990 in the west (sci:sha256:b4d3d3f5...). CMIP6 models change O2 on this surface less than observed (sci:sha256:66c86fe2..., sci:sha256:cc75ea4e...). A sibling job (sci:sha256:84f111c0..., published while this work ran) showed with EN4 and ship data that the winter outcrop of sigma0 26.5 shrank, and that 4 of 7 single CMIP6 runs have no outcrop. That study did not use model O2 or water age, and it could not bundle its EN4 series.

We asked three questions:

1. Does a public-domain climatology (World Ocean Atlas 2023, decadal fields) also show the outcrop loss?
2. In a large set of CMIP6 models, how often is the outcrop of the 26.4-26.7 class missing, and why?
3. Across models, does the outcrop size control the water on sigma0 26.5 in the northeast Pacific (depth, ideal age, apparent oxygen utilization AOU, O2)? This is the link that makes a missing outcrop a reason for the missing O2 loss.

Main results:

- **WOA23 shows the outcrop loss.** The area of the open North Pacific with late-winter (January-April maximum) surface sigma0 in 26.4-26.7 fell from 2.74 x 10^12 m2 (mean of 1965-1974 and 1975-1984) to 1.07 x 10^12 m2 (2005-2014 and 2015-2022), -61%. The area with sigma0 >= 26.5 fell from 1.57 to 0.22 x 10^12 m2 (-86%). Without the sparse 1975-1984 decade the changes are -49% and -83%. In March, at 38-48 N, 150-170 E, surface sigma0 fell from 26.48 to 26.32 kg/m3 (temperature +0.60 deg C, salinity -0.10). The largest decrease came between 1975-1984 and 1995-2004, before and during the downstream O2 decline (Fig. 1).
- **Most CMIP6 models do not outcrop this class.** In 40 historical runs (one member each), the 1985-2014 outcrop area was below 25% of WOA23 (1.19 x 10^12 m2, 1991-2020) in 23 runs and below 10% in 19 runs (13 of 24 model families below 25%). In the outcrop box the median March surface sigma0 bias was -0.27 kg/m3, from a median warm bias of +0.37 deg C and a fresh bias of -0.21. Seven runs had a larger outcrop than observed (Fig. 2).
- **Across models, the outcrop size predicts the water on sigma0 26.5 off California.** Spearman rank correlations of the outcrop area (26.4-26.7) with CalCOFI-box properties were: O2 +0.72 (n = 10 runs, one-sided permutation p = 0.011; 9 model families: +0.82, p = 0.006), AOU -0.67 (p = 0.019; families -0.80, p = 0.007), ideal age -0.66 (n = 13, p = 0.008; 8 families -0.43, p = 0.15) and the depth of sigma0 26.5 in the northeast Pacific -0.58 (n = 12, p = 0.024; with the area >= 26.5: -0.76, p = 0.003). Runs with an outcrop of at least 25% of WOA23 had CalCOFI O2 of 81-99 umol/kg. Runs without it had 6-81 umol/kg (median 51). All 10 runs in the test had less O2 at CalCOFI on this surface than WOA23 (105 umol/kg). GFDL-CM4 (0.25-degree ocean; snapshot only, its surface run was stopped) had 123 umol/kg. In runs without the outcrop the 26.5 surface in the northeast Pacific lies 40-280 m deeper than in WOA23, and in the CESM2 family the water there is 750-830 years old (Fig. 3).
- **No model with an outcrop reproduces the observed outcrop loss.** In the seven runs with a 1965-1984 outcrop of at least half the observed area, the 2005-2014/1965-1984 ratio of the outcrop area was 0.73-0.97 (area >= 26.5: 0.61-1.00). WOA23 gives 0.39 (0.14 for >= 26.5) (Fig. 4).
- **Model changes and lags do not settle the dynamics.** Across the 7 runs with annual O2 samples, the 1985-1994 to 2005-2014 O2 change did not correlate in a consistent way with the outcrop change. Single-run lag correlations of O2 with the outcrop area (1980-2014) had scattered best lags (0-20 yr), and they were also positive in runs with almost no outcrop. These tests are inconclusive. A multi-member IPSL-CM6A-LR test was planned but not done (see Limitations).

Interpretation: the sigma0 26.5 surface off California is ventilated through the late-winter outcrop in the northwestern Pacific. Climate models that have this outcrop have younger, oxygen-richer water on 26.5 off California. Models without it (most models, mostly because the subarctic-frontal surface water is too warm and too fresh) have old or deep water there. Their O2 on 26.5 cannot respond to a change of outcrop ventilation, and their mean O2 is too low. The models that do have an outcrop lose much less of it than the real ocean did after 1980. Both facts give a reason why CMIP6 historical runs do not make the observed sigma0 26.5 O2 loss. They add to the low AOU per year of age found earlier (sci:sha256:66c86fe2...). The cross-model relation is a mean-state relation in 10-13 runs. It does not prove that the outcrop loss caused the observed O2 loss.

![Observed outcrop](files/figures/fig1_observed_outcrop.png)

## Question, hypotheses and tests

Plan: `files/analysis_plan.md` (written before any CMIP6 outcrop value; addenda A and B list the changes).

| Test | Hypothesis | Prediction | Result |
|---|---|---|---|
| T1 observed outcrop | The 26.4-26.7 outcrop shrank | A_band and A_ge both fall by more than 30%, 1965-1984 to 2005-2022 | Supported: -61% and -86% (without 1975-1984: -49%, -83%) |
| T2 model mean state | Models without outcrop do not ventilate 26.5 | Outcrop area correlates negatively with age, AOU and depth, positively with O2 | Supported for O2, AOU, depth (models and families) and age (models; families not significant) |
| T2 counts | CMIP6 outcrop is realistic | Few models below 25% of WOA23 | Rejected: 23 of 40 runs below 25% |
| T3 model change | Model outcrop changes like the observed one | Ratio 2005-2014/1965-1984 near 0.39 | Rejected: 0.73-0.97 in all 7 runs with an outcrop |
| T3 cross-model change | Models with more outcrop loss lose more O2 | Positive rank correlation | Inconclusive (n = 4-7, signs differ by region) |
| T4 within-model lag | O2 follows the outcrop area with a lag | Consistent positive lag in runs with outcrop | Inconclusive (scattered lags, also positive without outcrop) |
| T5 scaling (exploratory) | Model O2-outcrop slope explains the observed loss | Model slope x observed outcrop change near the observed loss | Weak: -9.8 umol/kg (r = 0.34, n = 7) against a downstream loss of 20-38 |

## Data

- **World Ocean Atlas 2023** (NOAA NCEI, public), 1-degree monthly (January-April) temperature and salinity for the decades 1955-1964 to 2015-2022 and for 1991-2020; annual 1991-2020 temperature and salinity; annual all-period oxygen. URLs: `files/provenance/woa23_urls.txt`; SHA-256: `files/provenance/woa23_sha256.txt`. Downloaded 2026-11-10 to local scratch.
- **CMIP6 historical runs** (Pangeo CMIP6 public Zarr store on Google Cloud; 39 models CC BY 4.0, 3 GISS models CC0 1.0). Surface: Omon tos and sos, January-April 1950-2014, 42 runs (two removed by an area check, see Methods). Interior: Omon thetao, so, agessc and o2, April 2005, 13 runs. Store URLs, versions and the SHA-256 of each chunk: `files/provenance/cmip6_surface.json`, `files/provenance/cmip6_interior.json`; catalog hash in `files/provenance/inputs.json`.
- **Prior campaign publications** (used as published, read from the campaign ZIPs): annual CMIP6 samples on sigma0 26.5 at the CalCOFI box and North Pacific lines, 1980-2014 (sci:sha256:66c86fe2...); April model samples (sci:sha256:cc75ea4e...); WOD ship O2 band series on sigma0 26.5 (sci:sha256:b4d3d3f5..., Fig. 1c only). ZIP hashes: `files/provenance/inputs.json`.

Terms and attribution: `files/NOTICE_external_data.md`. No raw external data file is in the bundle.

## Methods

1. **Surface density** (`outcrop.py`, `woa_outcrop.py`, `model_outcrop.py`). TEOS-10 (gsw 3.6.23) sigma0 from SST and SSS. The late-winter field is the maximum over January-April of monthly sigma0 (WOA23: of the monthly climatology of each decade; models: of each year, and of the decadal monthly-mean climatology for comparison with WOA23).
2. **Outcrop metrics** (`outcrop.py`). Open North Pacific mask: 25-55 N, 120 E-125 W without the Sea of Japan, the East China Sea, the Sea of Okhotsk and the Bering Sea. A_band = area with 26.4 <= sigma0 < 26.7 (the band of Mecking and Drushka 2024, doi:10.5194/bg-21-1117-2024); A_ge = area with sigma0 >= 26.5. Cell areas: areacello; for runs without areacello, an area from cell spacing. Quality check: the mask area must agree with WOA23 (24.8 x 10^12 m2) within 10%. NESM3 and MCM-UA-1-0 failed (119 and 0.16 x 10^12 m2) and are excluded. March T, S and sigma0 means in 38-48 N, 150-170 E (the outcrop box) give the bias.
3. **Water on sigma0 26.5** (`cmip_interior.py`, `interior_boxes.py`). For April 2005, each column in 10-60 N, 110 E-100 W is interpolated linearly in sigma0 to 26.5 at the first crossing from the surface (depth, ideal age, O2 in umol/kg with in-situ density, O2 saturation from gsw.O2sol_SP_pt, AOU). Boxes: CalCOFI 29-35 N, 116-125 W; NEP 25-45 N, 160-120 W; cos(latitude) weights. WOA23 gives the observed values (annual T, S 1991-2020; O2 all periods). For four runs without a snapshot (IPSL-CM6A-LR, MIROC-ES2L, MPI-ESM-1-2-HAM, UKESM1-0-LL) the CalCOFI values are the 1985-2014 means of the published samples of sci:sha256:66c86fe2... (same box). Where both sources exist they agree (ACCESS-ESM1-5 age 167 vs 166 yr, O2 9 vs 7; CanESM5 age 552 vs 540 yr, O2 51 vs 49).
4. **Tests** (`analysis.py`). T2: Spearman rank correlation across runs and across model families (mean per family; families group runs with the same ocean model, list in `analysis.py`), one-sided p from 20,000 permutations. T3: ratio of the decadal-climatology outcrop area 2005-2014 to the mean of 1965-1974 and 1975-1984 in runs with a 1965-1984 outcrop of at least half of WOA23. T4: Pearson correlation of annual box O2 (1980-2014 samples) with annual A_band at lags 0-20 yr, raw and linearly detrended; no correction for the lag search. T5: least-squares slope of the 1985-1994 to 2005-2014 O2 change (North Pacific line bins) on the outcrop change.
5. **Figures** (`figures.py`).

## Results

### Observed outcrop by WOA23 decade (`files/results/woa_outcrop.csv`)

| Decade | A_band (10^12 m2) | A_ge 26.5 | Band cells with winter T+S data | March sigma0, 38-48 N 150-170 E | March T (deg C) | March S |
|---|---|---|---|---|---|---|
| 1955-1964 | 2.13 | 1.21 | 16% | 26.34 | 6.14 | 33.59 |
| 1965-1974 | 2.11 | 1.26 | 66% | 26.45 | 6.20 | 33.73 |
| 1975-1984 | 3.37 | 1.88 | 42% | 26.51 | 5.57 | 33.69 |
| 1985-1994 | 2.08 | 0.96 | 71% | 26.43 | 5.69 | 33.60 |
| 1995-2004 | 1.50 | 0.57 | 74% | 26.43 | 6.08 | 33.67 |
| 2005-2014 | 1.05 | 0.30 | 95% | 26.35 | 6.30 | 33.61 |
| 2015-2022 | 1.09 | 0.14 | 95% | 26.30 | 6.68 | 33.62 |
| 1991-2020 | 1.19 | 0.29 | 98% | 26.36 | 6.32 | 33.62 |

The outcrop lies at 38-52 N, 143-172 E (Fig. 1a). From 1965-1984 to 2005-2022 the 26.5 contour moved north and the band east of 165 E disappeared. WOA23 decadal fields relax to the all-decade first guess where data are sparse. This makes changes smaller, not larger, but the 1955-1964 and 1975-1984 values are uncertain. The EN4 and ship-cast estimates of sci:sha256:84f111c0... (area >= 26.5: -73% from 1984-1996 to 2009-2025; ship surface sigma0 -0.15 kg/m3) agree with these values.

### CMIP6 outcrop (`files/results/model_table.csv`, `model_outcrop_decadal.csv`, `model_outcrop_annual.csv`)

![Model outcrop](files/figures/fig2_model_outcrop.png)

Runs with an outcrop larger than observed (CNRM-CM6-1, IITM-ESM, CNRM-ESM2-1, MRI-ESM2-0, IPSL-CM6A-LR, FGOALS-g3, GFDL-ESM4) have March surface water in the outcrop box that is about right or too dense (+0.02 to +0.44 kg/m3). All 23 runs without an outcrop have lighter water (-0.17 to -0.92 kg/m3); 19 of them are too warm and 19 too fresh (Fig. 2b).

### Outcrop and the water on sigma0 26.5 (`files/results/interior_boxes.csv`, `tests.json`)

| Run | Outcrop 26.4-26.7 (10^12 m2) | Area >= 26.5 | March sigma0 bias | Depth of 26.5, NEP (m) | Ideal age, CalCOFI (yr) | AOU, CalCOFI | O2, CalCOFI |
|---|---|---|---|---|---|---|---|
| WOA23 (observed) | 1.19 | 0.29 | 0 | 338 | - | 181 | 105 |
| CNRM-ESM2-1 | 3.97 | 4.58 | +0.42 | 269 | - | 189 | 81 |
| IPSL-CM6A-LR* | 2.93 | 2.03 | +0.16 | - | 98 | 174 | 99 |
| GFDL-ESM4 | 2.12 | 0.88 | +0.02 | 401 | - | 203 | 90 |
| GISS-E2-1-G | 0.51 | 0.29 | -0.09 | 366 | 226 | - | - |
| MPI-ESM-1-2-HAM* | 0.28 | 0.14 | -0.17 | - | 365 | 212 | 67 |
| ACCESS-ESM1-5 | 0.27 | 0.00 | -0.35 | 522 | 167 | 271 | 9 |
| MIROC-ES2L* | 0.01 | 0.00 | -0.40 | - | 365 | 194 | 81 |
| UKESM1-0-LL* | 0.01 | 0.01 | -0.39 | - | 96 | 277 | 12 |
| CanESM5 | 0.01 | 0.01 | -0.24 | 428 | 552 | 226 | 51 |
| CanESM5-CanOE | 0.01 | 0.01 | -0.24 | 428 | 508 | 197 | 80 |
| CMCC-ESM2 | 0.00 | 0.00 | -0.35 | 380 | - | 281 | 6 |
| CESM2-WACCM-FV2 | 0.00 | 0.00 | -0.47 | 475 | 831 | - | - |
| ACCESS-CM2 | 0.00 | 0.00 | -0.35 | 622 | 125 | - | - |
| CESM2 | 0.00 | 0.00 | -0.53 | 470 | 754 | - | - |
| CESM2-WACCM | 0.00 | 0.00 | -0.54 | 464 | 758 | - | - |
| CESM2-FV2 | 0.00 | 0.00 | -0.54 | 457 | 809 | - | - |

O2 and AOU in umol/kg. * CalCOFI values from the 1985-2014 samples of sci:sha256:66c86fe2...; others from the April 2005 snapshot. GFDL-CM4 has a snapshot (depth 325 m in the NEP box; CalCOFI O2 123, AOU 170) but no surface run (stopped, see Limitations), so it is not in the tests. CanESM5 and CanESM5-CanOE share the same physical ocean (identical outcrop), so they count as one family.

![Outcrop vs interior](files/figures/fig3_outcrop_vs_interior.png)

| Pair (outcrop metric ~ property) | Runs: rho (p) | Families: rho (p) |
|---|---|---|
| A_band ~ O2 CalCOFI | +0.72 (0.011), n = 10 | +0.82 (0.006), n = 9 |
| A_ge ~ O2 CalCOFI | +0.74 (0.010) | +0.78 (0.010) |
| A_band ~ AOU CalCOFI | -0.67 (0.019), n = 10 | -0.80 (0.007), n = 9 |
| A_band ~ ideal age CalCOFI | -0.66 (0.008), n = 13 | -0.43 (0.15), n = 8 |
| A_band ~ ideal age, North Pacific lines 1985-2014 | -0.83 (0.008), n = 8 | -0.61 (0.07), n = 7 |
| A_band ~ depth of 26.5, NEP | -0.58 (0.024), n = 12 | -0.52 (0.12), n = 7 |
| A_ge ~ depth of 26.5, NEP | -0.76 (0.003), n = 12 | -0.70 (0.045), n = 7 |
| March sigma0 (box) ~ O2 CalCOFI | +0.64 (0.025), n = 10 | +0.68 (0.023), n = 9 |

Exceptions: UKESM1-0-LL and ACCESS-CM2 have no outcrop but young water (96 and 125 yr). Their 26.5 surface must be ventilated in another way (for example from the masked marginal seas or north of 55 N). UKESM1-0-LL nevertheless has very low O2 (12 umol/kg), so its oxygen use is high. The outcrop is thus one strong control of the mean state, not the only one.

### Outcrop change in models (`tests.json` T3)

![Outcrop change](files/figures/fig4_outcrop_change.png)

| Run | A_band ratio 2005-2014 / 1965-1984 | A_ge ratio |
|---|---|---|
| WOA23 (2005-2022) | 0.39 | 0.14 |
| CNRM-CM6-1 | 0.82 | 0.75 |
| CNRM-ESM2-1 | 0.77 | 0.74 |
| FGOALS-g3 | 0.85 | 0.87 |
| GFDL-ESM4 | 0.97 | 1.00 |
| IITM-ESM | 0.94 | 0.92 |
| IPSL-CM6A-LR | 0.73 | 0.61 |
| MRI-ESM2-0 | 0.89 | 0.83 |

With WOA23 2005-2014 alone the observed ratio is 0.38. The CMIP6 median outcrop fell from 0.3-0.6 to near 0 x 10^12 m2 because the small outcrops of many runs disappeared (Fig. 4).

### Changes and lags (`tests.json` T3-T5, `lag_test.csv`)

Across 7 runs with annual samples, the rank correlation of the 1985-1994 to 2005-2014 O2 change with the outcrop change was -0.13 (CalCOFI) and +0.38 (North Pacific lines), with p > 0.19. The mean outcrop area correlated with the CalCOFI O2 change at -0.74 (p = 0.03), but with the North Pacific line change at +0.70 (opposite sign). The slope of O2 change on outcrop change (T5) was 3.0 umol/kg per 10^12 m2 (r = 0.34), which gives -9.8 umol/kg for the observed outcrop change. Single-run lag correlations (detrended) reached 0.3-0.6 at lags from 0 to 20 yr, in runs with and without an outcrop. We do not interpret these as a lag.

## Limitations

- The cross-model relation uses 10-13 runs (8-9 families) and single members. It is a relation of mean states. It does not show that a change of outcrop caused the observed O2 loss. Model families are not fully independent.
- Interior values come from one month (April 2005) for 9 runs and from 1985-2014 annual samples for 4 runs. Ideal age changes slowly, but O2 has year-to-year noise of a few umol/kg.
- The outcrop is a surface proxy for subduction. We did not calculate mixed-layer depth, subduction rate or preformed O2.
- WOA23 decadal fields are objective analyses; data coverage in the outcrop band was 16-42% in 1955-1964 and 1975-1984. The 1975-1984 maximum is uncertain. The main change (-49% for A_band, -83% for A_ge without 1975-1984) does not depend on it.
- The shared host's download rate from the CMIP6 store fell to 0.1-0.3 MB/s during this job. We stopped the planned 6-10-member IPSL-CM6A-LR ensemble test (code in `files/code/not_run/`, no result), the surface runs of 7 high-resolution or late models (CMCC-CM2-HR4, CNRM-CM6-1-HR, GFDL-CM4, HadGEM3-GC31-MM, INM-CM4-8, MPI-ESM1-2-HR, NorESM2-MM; NorCPM1 was incomplete) and the interior snapshots of 15 runs. AWI models (unstructured grid) are not supported by the code.
- Two runs (NESM3, MCM-UA-1-0) failed the area check and are excluded.
- The observed interior values (WOA23 O2 all periods, T and S 1991-2020) are climatologies, not 2005 values.

## Reproduction

`files/code/run_all.sh SCRATCH CAMPAIGN_DIR` runs the full pipeline. It downloads about 2.6 GB of WOA23 and about 20-40 GB of CMIP6 chunks into SCRATCH (nothing into the publication folder), reads the three prior campaign ZIPs, and writes results and figures to SCRATCH. The exact runs are in `files/code/runlist_surface.txt` and `runlist_interior.txt`. Python 3.12 with the versions in `files/code/requirements.txt`; gsw and numcodecs go in a private folder given by EXTRA_PYLIB. Set `OMP_NUM_THREADS=1`. On hosts where IPv6 routes to storage.googleapis.com hang, `cmip_surface.py` forces IPv4.

Bundled derived results: `files/results/` (outcrop metrics per WOA23 decade, per model decade and per model year; interior box values; the model table; all test statistics in `tests.json`; 1-degree maps of winter-maximum sigma0 and of sigma0 26.5 properties as `.npz`).

## Attribution

Text, figures, code and derived results: SCI baseline license (see LICENSE). WOA23: NOAA NCEI. CMIP6: WCRP and the modelling groups (CC BY 4.0; GISS CC0 1.0), via the Pangeo CMIP6 cloud copy. Full notice: `files/NOTICE_external_data.md`.
