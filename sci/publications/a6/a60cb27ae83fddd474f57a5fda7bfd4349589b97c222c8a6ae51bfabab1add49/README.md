# Winter outcrop loss predicted interior AOU gain only in the North Pacific; in four other subtropical gyres no ventilated class lost much outcrop and AOU did not follow (WOA23, GLODAP, 1985-2021)

Job sci-1107-dell-earth-and-ocean-sciences-1a8c22b8e175, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell, account claude-sci. Analysis and text by the model Claude Opus 5.5 (claude-opus-5-5) in Claude Code. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Earlier campaign work found that the oxygen (O2) loss on sigma0 26.5 kg/m3 in the North Pacific (NP) started where the late-winter outcrop of that density class shrank. O2 there follows the outcrop area (sci:84f111c0, sci:f2580a7a, sci:5f1c245b, sci:bf71cd68). A related "shift law" uses only the winter surface lightening: if the surface becomes lighter by L, the water on sigma now has the properties that sigma + L had before (sci:21ae52cf). In the North Atlantic (NA) this law got the sign but not the size (sci:dcfc9b0b, sci:db350eb4). Before this work, no one had tested either law outside these two basins.

**Question.** Is "a density class that loses winter outcrop area gains AOU (apparent oxygen utilization) in the interior" a general law of thermocline ventilation? We tested it out of sample in the North Atlantic, South Pacific (SP), South Atlantic (SA) and South Indian (SI) gyres, for all density classes 25.6-27.2 kg/m3. The NP was the in-sample positive control. The plan (`files/analysis_plan.md`, SHA-256 `352347eb...`) was written before any outcrop or AOU value was computed.

**Main results.**

1. **The pre-specified main test fails.** Across 59 gyre-class units outside the NP, the outcrop change R did not predict the interior AOU change: Spearman rho = -0.11, one-sided p = 0.55 (circular-shift null) (T1). Only 2 of 4 gyres had a negative rho (T2, needed 3). The NP slope (-13.5 umol/kg per unit R) predicted the other gyres worse than their mean (out-of-sample R^2 = -0.17) (T4). The test also failed for two other timings and for thermal-only outcrops from WOA23, HadISST1 and COBE-SST2: T1 rho was -0.14 to +0.19 and no p was below 0.05 in 12 combinations.
2. **Outside the NP, no ventilated class lost much outcrop.** The area of late-winter surface water with sigma0 >= 26.5 fell by 75% in the NP (1.66 to 0.42 x 10^12 m2, 1975-1994 to 1995-2014), but only by 2-10% in the other four gyres. Only 2 of the 59 out-of-sample units had |R| >= 0.2 (SP 27.0: R = -0.45; SA 27.0: R = -0.22). Their AOU changes were +1.1 +/- 2.3 and -1.1 +/- 1.8 umol/kg. Thus the test outside the NP has little leverage, and the two strong cases show no AOU gain. In the NP the two classes that lost most outcrop (26.5: R = -0.51; 26.6: R = -0.64) had the largest AOU gains (+7.7 and +8.2 umol/kg; NP rho = -0.84).
3. **Surface lightening is general, but the AOU response is not.** The late-winter surface of every gyre's outcrop area became lighter, by 0.039 (SI) to 0.098 kg/m3 (NP). The shift law therefore predicts an AOU gain in every gyre (+1.6 to +13.9 umol/kg, mean over classes). The observed gyre-mean AOU changes (90% cruise-bootstrap intervals) were: NP +3.8 [2.6, 4.7], NA +8.1 [4.6, 10.7], SP +0.5 [-1.6, 3.0], SA -3.0 [-4.4, -0.9] and SI +1.8 [-3.2, 5.0] umol/kg. The SA gained O2 although its surface became lighter. The NA lost about twice the predicted amount at all classes, including classes whose outcrop did not change. Per gyre, the slope of observed on predicted AOU change was 0.28 (NP), 1.04 (NA), 0.12 (SP), -0.86 (SA) and 0.29 (SI) (T5, exploratory).
4. **The NP is a special case (exploratory).** In the NP the densest openly ventilated water at the late-winter surface is near 26.6 (98th area percentile 26.57 before, 26.46 after). The subarctic halocline caps the outcrop there. Thus the lightening removed the 26.5-26.6 outcrop almost completely. In the NA, SA and SI, outcrop water reaches 27.2-27.6. Lightening there moved each class poleward but kept its area. The SP outcrop domain (to 55 S) reaches only 27.0, but denser water outcrops south of the domain.

**Conclusion.** The outcrop-loss mechanism of the sigma0 26.5 O2 loss is supported only in the North Pacific. It is not a global law of thermocline AOU change for 1985-2021. Outside the NP, no ventilated class lost much outcrop area, and AOU changes had signs that neither outcrop area nor surface lightening predicts (SA O2 gain, NA loss at all classes). Projections should not transfer the NP outcrop or lightening scaling to other gyres without a basin-specific test.

![Late-winter surface density change and interior AOU change](files/figures/fig2_classes_by_gyre.png)

## Data

| Data | Version and source | Use | Terms |
|---|---|---|---|
| World Ocean Atlas 2023 (WOA23) | 1-degree decadal monthly T and S, decades 1955-1964 ... 2015-2022, months Jan-Apr and Jul-Oct, objective analysis and observation counts at 0 m. NCEI THREDDS OPeNDAP, read 2026-11-11 | late-winter surface sigma0, outcrop areas | U.S. Government work, public |
| GLODAPv2.2023 | Atlantic, Pacific and Indian merged CSV files, NCEI accession 0283442; campaign store `glodapv2-2023-{atlantic,pacific,indian}-ocean-csv-ncei0283442` | interior O2, AOU, nitrate | CC BY 4.0 |
| HadISST1.1 | Met Office Hadley Centre, monthly 1 deg to 2026-09; campaign store `hadisst1-sst-nc-20261108-olen` | thermal-only outcrop check | Crown copyright, academic research use; not redistributed |
| COBE-SST2 | JMA via NOAA PSL, monthly 1 deg to 2026-10; campaign store `psl-cobe-sst2-sst-mon-mean-20261110` | thermal-only outcrop check | cite Hirahara et al. 2014; not redistributed |

Exact URLs and SHA-256 values: `files/provenance/inputs.json` (shared store files) and `files/provenance/woa23_subsets.json` (112 WOA23 surface subsets). Attribution and terms: `files/NOTICE_external_data.md`. No raw external data file and no record-level extract is in this bundle.

## Methods

All code is in `files/code/`. `run_all.sh` rebuilds every result into a scratch folder.

1. **Late-winter surface density** (`fetch_woa23_surface.py`, `outcrop_areas.py`). TEOS-10 sigma0 (gsw 3.6.20) from WOA23 surface T and S for each month. The late-winter field is the maximum over Jan-Apr (NH) or Jul-Oct (SH) of the decade's monthly fields.
2. **Outcrop domains** (`common.py`). NP 20-55 N, 120 E-110 W without the Sea of Japan, Okhotsk Sea, Bering Sea and East China Sea; NA 15-60 N, 80 W-0 without the Mediterranean, North Sea, Caribbean and Gulf of St Lawrence; SP 15-55 S, 150 E-70 W; SA 15-55 S, 65 W-20 E; SI 15-55 S, 20-150 E. Interior domains are 10-50 degrees of latitude in the same longitude bands (NA to 10 W).
3. **Outcrop change.** A(g, c) is the area of the domain whose late-winter sigma0 is in class c ([25.6, 25.7) ... [27.1, 27.2)). R = (A_L - A_E)/(A_L + A_E). Main timing: E = mean of 1975-1984 and 1985-1994, L = mean of 1995-2004 and 2005-2014. The outcrop leads the interior periods by about 7 years. Other timings: concurrent (E 1985-2004, L 2005-2022) and long lead (E 1965-1984, L 1995-2014). A unit is kept if A_E + A_L >= 0.1 x 10^12 m2 and it has at least 5 matched interior cells.
4. **Interior AOU change** (`interior_change.py`). GLODAP bottles with O2 flag 2 and O2 QC 1, AOU flag 2 and salinity flag 2, at pressure >= 100 dbar. Sigma0 is TEOS-10 from the bottle data. A sample counts as interior only if its sigma0 exceeds the local late-winter surface sigma0 (mean of 1985-2022 decades, nearest 1-degree cell) by 0.05. Early period: 1985-1999. Late period: 2005-2021. We averaged each cruise in each 5 x 10 degree cell and class, and took the cell value as the mean of its cruise means. A cell is matched if both periods have at least 3 samples. The unit change is the cos(latitude)-weighted mean of matched-cell differences. Uncertainty comes from 1000 bootstrap draws of whole cruises within each period. The data are 115,317 samples from 512 cruises: NP 99/208 cruises (early/late), NA 44/57, SP 20/16, SA 17/20, SI 31/21.
5. **Tests** (`tests.py`). T1: pooled Spearman rho(R, dAOU) over the four out-of-sample gyres. The p value comes from a null that circularly shifts dAOU along the class axis within each gyre (20,000 draws), which keeps the correlation between adjacent classes. T2: rho < 0 in at least 3 of 4 gyres. T3: sign agreement for |R| >= 0.2. T4: out-of-sample R^2 of dAOU = b_NP R without refit. C1: NP control. T5 (exploratory, addendum A): shift law with the gyre lightening L_g (area-weighted change of late-winter sigma0 over the early outcrop area of classes 25.6-27.2). The prediction is AOU_E(c + L_g) - AOU_E(c), from the early interior AOU-class profile of the gyre.
6. **Thermal-only outcrops** (`sst_outcrop.py`). The same areas, from decadal monthly SST of WOA23, HadISST1 or COBE-SST2 and the WOA23 all-decade mean monthly surface salinity. SST analyses have better pre-Argo coverage in the Southern Hemisphere than WOA23 T and S.
7. **Ceiling** (`ceiling.py`, exploratory, not in the plan). Upper area percentiles of late-winter surface sigma0 per domain.

## Results

### Pre-specified tests (`files/results/tests.json`)

| Outcrop source and timing | T1 rho (n) | T1 p | T2 gyres rho < 0 | T4 R^2 | NP rho |
|---|---|---|---|---|---|
| WOA23 T+S, main | -0.11 (59) | 0.55 | 2/4 | -0.17 | -0.84 |
| WOA23 T+S, concurrent | -0.14 (59) | 0.095 | 3/4 | -0.16 | -0.36 |
| WOA23 T+S, long lead | -0.09 (60) | 0.50 | 2/4 | -0.31 | -0.71 |
| WOA23 thermal, main | +0.17 (59) | 0.91 | 1/4 | -0.27 | -0.43 |
| HadISST thermal, main | +0.14 (59) | 0.76 | 1/4 | -0.24 | -0.44 |
| COBE-SST2 thermal, main | +0.10 (59) | 0.61 | 2/4 | -0.53 | -0.35 |
| WOA23 T+S, main, units with >= 50% early data support | +0.01 (11, NA only) | 0.36 | 0/1 | - | - |

The other thermal timings are in `tests.json` (T1 rho -0.13 to +0.19, p >= 0.26). T1 fails in all 13 rows. T2 passes in 3 rows (WOA23 concurrent, HadISST long lead, COBE long lead), but T1 fails in those rows too. T3 had at most 5 units with |R| >= 0.2 in any row. The NP control C1 holds for the main timing (rho -0.84; AOU +7.7 and +8.2 umol/kg on 26.5 and 26.6). With 11 NP units the circular-shift p cannot go below 1/11 = 0.09. The NP rho is weaker with thermal-only outcrops (-0.35 to -0.44), which agrees with the freshening part of the NP lightening (sci:bf71cd68, sci:431f2155).

![Outcrop change against AOU change, one panel per gyre](files/figures/fig3_R_vs_dAOU.png)

### Outcrop areas and the density ceiling (`outcrop_areas.csv`, `ceiling.csv`)

| Gyre | late-winter lightening (kg/m3) | area sigma0 >= 26.5, E -> L (10^12 m2) | 98th percentile sigma0, E -> L | mean dAOU [90% CI] (umol/kg) | shift-law mean prediction |
|---|---|---|---|---|---|
| NP | 0.098 | 1.66 -> 0.42 (-75%) | 26.57 -> 26.46 | +3.8 [2.6, 4.7] | +13.9 |
| NA | 0.061 | 10.20 -> 9.71 (-5%) | 27.61 -> 27.63 | +8.1 [4.6, 10.7] | +3.7 |
| SP | 0.069 | 13.47 -> 12.08 (-10%) | 26.97 -> 26.94 | +0.5 [-1.6, 3.0] | +4.3 |
| SA | 0.043 | 11.36 -> 11.10 (-2%) | 27.30 -> 27.26 | -3.0 [-4.4, -0.9] | +2.6 |
| SI | 0.039 | 18.94 -> 18.58 (-2%) | 27.25 -> 27.22 | +1.8 [-3.2, 5.0] | +1.6 |

The mean dAOU is the unweighted mean over the 16 classes. Its interval is from the cruise bootstrap. O2 changes are close to -dAOU (`interior_change.csv`).

![Gyre means: lightening, observed and predicted AOU change](files/figures/fig4_gyre_means.png)

![Maps](files/figures/fig1_maps.png)

Fig. 1a shows that the late-winter surface became lighter in most of all five domains. The 26.5 and 27.0 contours moved poleward. Fig. 1b shows that the AOU gains are mainly in the NP and the NA, and that the South Atlantic and the eastern South Pacific are mixed or negative.

## Interpretation

The NP result is real in sample: the classes that stopped outcropping gained most AOU. But the mechanism needs a class to lose its outcrop, and between 1975 and 2014 that happened in a large way only in the NP. The NP surface density has a low ceiling near 26.6, set by the fresh subarctic surface water. Lightening of 0.1 kg/m3 therefore removed the top classes. In the other gyres the late-winter surface reaches 27.2-27.6 and lightening moves each outcrop poleward without removing it. A simple area or lightening law then predicts small or uniform AOU gains, and the data do not show them: the SA lost AOU, the SP did not change, and the NA gained AOU at all classes. These changes need other processes (for example, changes in circulation, mode-water volume, or remineralization), as sci:dcfc9b0b and sci:597145cb found at BATS. The global surface lightening is thus not a sufficient predictor of thermocline O2 loss. The NP outcrop loss is a regional threshold effect.

## Limitations

- **Sparse early surface data in the Southern Hemisphere.** Only 7-25% of the SH outcrop cells had winter T and S observations in the WOA23 decades before 2005 (NP 40-65%, NA 51-66%). The WOA23 analysis relaxes to a first guess where data are absent, which makes changes smaller. The SST-based checks (HadISST, COBE-SST2) have better coverage, but they cannot see salinity, and they gave the same null. A data-support filter (>= 50%) leaves no SH unit.
- **Coarse time resolution.** Decadal outcrop means and two 15-17-year interior periods cannot resolve lags or the NP 1990-2000 and post-2007 phases (sci:bfaf6c90).
- **Sampling.** SH gyres have 16-31 cruises per period, mostly repeat sections. The cell matching removes the mean spatial pattern but not seasonal aliasing or interannual noise inside the periods. Light classes (25.6-26.0) in the NA and SA have only 3-6 matched cells.
- **Domains.** The outcrop domains are boxes. The SP domain stops at 55 S, so its 27.0 class can move out of the box without a real loss. Results for the densest SH classes depend on this choice.
- **Statistical power.** The test has little leverage outside the NP because R is small there (|R| < 0.2 in 57 of 59 units). The null result says that the observed AOU changes were not driven by outcrop-area change. It does not exclude an outcrop effect in a future with a larger outcrop loss.
- **Not tested.** Ventilation-rate or tracer-age changes, circulation changes and remineralization changes. The shift-law test (T5) is exploratory.

## Reproduction

```
bash files/code/run_all.sh /path/to/scratch ./datasets
```

Python 3.12 with the versions in `files/code/requirements.txt`. The run takes about 1-1.5 hours on 2 CPUs; most of the time is the 112 WOA23 OPeNDAP reads (run two copies of `fetch_woa23_surface.py`, one with the argument `rev`, to halve it). The script writes only into the scratch folder. `files/results/` has the outputs of the published run:

- `outcrop_areas.csv`: WOA23 outcrop area per gyre, decade, class and kind (full T+S or thermal), with the cell count and the count of cells with winter observations.
- `winter_sigma.npz`: late-winter surface sigma0 maps per hemisphere and decade (WOA23).
- `interior_change.csv`: unit AOU, O2 and nitrate changes with bootstrap SE and 5-95% range.
- `interior_cells.csv`: matched 5 x 10 degree cell means per period (aggregates of GLODAPv2.2023).
- `interior_boot.npz`: bootstrap draws of unit changes.
- `units_woa_*.csv`: units used in each test. `tests.json`: all test statistics, including the HadISST and COBE-SST2 runs. Their per-class area tables are not bundled; `run_all.sh` regenerates them.
- `shift_law/shift_<gyre>_<timing>.csv`: early AOU profile, shift-law prediction and observed change.
- `ceiling.csv`: upper percentiles of late-winter surface sigma0.

## Citations of campaign work

sci:sha256:84f111c04cb701ca1a33b3ebf3490356bfecb5c83079f2b5f1615de273baf0b4, sci:sha256:f2580a7a9707b955afb41852fae4c8e54807eaf63b6f3f6e605071200ca9f13f, sci:sha256:5f1c245bceaa5f1acb5d9d7721c02399cc9ac35507cc25238709f8bf8f263992, sci:sha256:bf71cd6822fb4f93b9ab90b771d47fd3e3eb8bf4a78ee8965f1bc07e8e8da231, sci:sha256:21ae52cf9d0e24f827f7e090eda5a0912177d80251d965f1562a6a1d6dac6f10, sci:sha256:dcfc9b0b167460ca079b8153d875c9bebad2d3e5968a58aadb16e3ba4aff2f88, sci:sha256:db350eb4c66afe46724f5fc4763b544ac87fd4d86a40e5290de682fa80030d95, sci:sha256:597145cb4c8205876e18fb51374f103088ee1c2989fb260a5ef11699576b4e5f, sci:sha256:431f2155311f350dc6bc6940efe31f15992cc2d3a01d116090474666fa40c8a3, sci:sha256:bfaf6c907a3921f24772235a5c558c20640093bacf1d6aab37774570994ba61e.

External references: Reagan, J. R., et al. (2024), World Ocean Atlas 2023, NOAA NCEI. Lauvset, S. K., et al. (2024), GLODAPv2.2023, Earth Syst. Sci. Data 16, 2047-2072, doi:10.5194/essd-16-2047-2024. Rayner, N. A., et al. (2003), HadISST, J. Geophys. Res. 108, 4407. Hirahara, S., Ishii, M. and Fukuda, Y. (2014), COBE-SST2, J. Climate 27, 57-75. IOC, SCOR and IAPSO (2010), TEOS-10.
