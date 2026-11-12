# In seven CMIP6 atmosphere models, the 1979-2014 radiation response to AMIPII-minus-HadISST2 SST differences is 1.2-4 times the Green's-function prediction, so GF artifact biases are probably too small

**Job** sci-1107-dell-earth-and-ocean-sciences-f1edccb24570 · **campaign** 11_07_2026 · **topic** earth-and-ocean-sciences · **machine** dell · **model** Claude Opus 5.5 (claude-opus-5-5) · **analysis date** 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Earlier campaign work found step artifacts in the SST forcing of atmosphere models (AMIPII / PCMDI-AMIP: the November 1981 HadISST1-to-OI v2 splice, OI v2 steps, NCEP sea-ice steps). It calculated their effect on radiative feedback with linear Green's functions (GFs) from GFMIP (sci:sha256:78d7f2e0, sci:sha256:36b3c230, sci:sha256:121acf9e, sci:sha256:990a6603, sci:sha256:642d8851). All these studies state the same limitation: "no full model runs". A GF is a linear map from SST patches to top-of-atmosphere (TOA) radiation. Nobody in the campaign tested whether real atmosphere models respond to SST-dataset differences as the GFs predict.

CMIP6 has a natural experiment for this test. The same atmosphere models ran two experiments over 1979-2014 with the same external forcing but different SST and sea-ice data:

- `amip` (CMIP): PCMDI-AMIP 1.1.3 (AMIPII = HadISST1 to Oct 1981, NOAA OI v2 after; NCEP-based sea ice).
- `highresSST-present` (HighResMIP): HadISST2.2.0.0 daily SST and sea ice (one homogeneous product with bias adjustments).

For each model, the difference dN = N(amip) - N(highresSST-present) is the model's own TOA response to the SST and sea-ice dataset difference, plus internal atmospheric noise. We asked:

1. Does dN follow the GF prediction from the SST difference dS that the model actually saw?
2. Is the response to the 1981 splice step as large as the GFs predict?
3. How large is the real-model effect of the dataset choice on 1979-2014 radiation trends?

## Main results

Seven same-model pairs (36 amip runs, 8 highresSST-present runs; Table 1). "5-GF" is the mean of the CAM5, CanESM5, ECHAM6, GFDL-AM4 and HadAM3 GFMIP Jacobians (as in sci:sha256:78d7f2e0); CAM4 (Dong et al. 2019) is also shown. The GF acts on dS in 60S-60N ice-free 5-degree boxes. A sea-ice term (CAM5 albedo kernel x surface-albedo difference, ocean poleward of 50 degrees) is added. Intervals are 95% (1.96 SE), Newey-West or AR(1)-adjusted.

**Table 1. Model pairs**

| Pair (amip / highresSST-present source_id) | amip members | hSST members | Same-family GF |
|---|---|---|---|
| CNRM-CM6-1 / CNRM-CM6-1 | 1 | 2 | none |
| CNRM-CM6-1-HR / CNRM-CM6-1-HR | 1 | 1 | none |
| GFDL-AM4 (C96) / GFDL-CM4C192 (C192 atmosphere) | 1 | 1 | GFDL-AM4 |
| HadGEM3-GC31-LL / HadGEM3-GC31-LM (both N96 atmosphere) | 5 | 1 | HadAM3 (ancestor) |
| HadGEM3-GC31-MM / HadGEM3-GC31-MM | 4 | 1 | HadAM3 (ancestor) |
| IPSL-CM6A-LR / IPSL-CM6A-LR | 21 | 1 | none |
| MPI-ESM1-2-HR / MPI-ESM1-2-HR (ECHAM6.3) | 3 | 1 | ECHAM6 |

1. **The real response is larger than the GF prediction (Figures 1 and 2).** We regressed dN on the 5-GF prediction and the sea-ice term. The scaling factor a is 1 if the GF is right.
   - Annual means, cubic time trend removed (removes slow forcing differences): a = 1.2 to 3.9, median 1.9; a > 1 in all 7 pairs, and the 95% interval is above 1 in 4 pairs. Without the volcanic periods (1982-04 to 1984-12, 1991-06 to 1993-12): a = 1.1 to 4.0, median 2.4 (all 7 above 1; 4 with the 95% interval above 1).
   - Monthly anomalies: a = 0.7 to 3.3, median 1.5 (with a cubic trend removed 0.9 to 2.4, median 1.3; without volcanic periods 1.0 to 3.1, median 1.6). Thus the excess is larger at annual and longer time scales.
   - With the GF of the same model family, the factor stays above 1: MPI-ESM1-2-HR with ECHAM6 a = 2.1 (monthly) and 3.6 (annual); GFDL-AM4 pair with GFDL-AM4 a = 1.8 and 1.4; HadGEM3 pairs with HadAM3 a = 1.7-2.0 and 1.8-2.8.
   - Of the six single GFs, only CAM4 (the most sensitive one) is near or above the real response (median a = 0.7 at annual scale).
   - Control: each run regressed on the GF prediction from its own full SST anomalies gives a = 0.0 to 1.2 (R2 at most 0.25). Thus the GFs do not generally under-predict these models. The excess is specific to the dataset-difference patterns.

2. **A decadal pattern change gives 1.2-6 times the predicted radiation change (Figure 3, Figure 4c).** From 1985-1990 to 1994-2008, the 60S-60N mean of dS does not change (within 0.004 K). But the pattern changes: AMIP becomes 0.09 K colder than HadISST2 in the warm pool, 0.13 K colder in the tropical Atlantic, 0.07 K colder in the NH extratropics, and 0.25 K warmer at 40-60S. The 5-GF prediction for this change is +0.14 to +0.15 W m-2 (CAM4 +0.30 to +0.32). The real change of dN is positive in all seven pairs: +0.17 to +0.92 W m-2 (median +0.46; 1.8 to 7.7 SE). The ratio to the 5-GF prediction (sea-ice term removed) is 1.2 to 6.1, median 3.3. In 5 of 7 pairs the change is larger than the CAM4 prediction. About half of the change is LW (+0.20 to +0.31) and half SW (-0.06 to +0.61). The real change is spread over the tropics and the SH subtropics, including the southeast Pacific and the south Indian Ocean (Figure 3c). The GF puts it in the west Pacific (Figure 3b).

3. **Regional sensitivities (Figure 4a).** A regression of monthly dN on six regional SST differences (pooled over pairs) gives -15.8 +/- 3.0 W m-2 per K for the warm pool (15S-15N, 40-180E; 5-GF -9.3, GF range -16.5 to -6.4), -4.4 +/- 3.4 for the east/central tropical Pacific (5-GF -1.2), +2.9 +/- 2.1 for 15-40S (5-GF -0.6) and +5.9 +/- 1.5 for 40-60S (5-GF -0.4, range -2.9 to +2.0). Thus, in these models, the warm pool has about 1.7 times the GF sensitivity, and Southern Ocean warming increases net downward radiation. Most GFs do not have this. The sea-ice coefficient is 0.75 +/- 0.18.

4. **The 1981 splice step (Figure 4b).** The step of dS at 1981-11 (34 months before, 60 after) correlates with the AMIP-minus-in-situ step map of sci:sha256:36b3c230 (pattern r = 0.64). It is larger here: warm pool +0.17 K, 60S-60N +0.06 K. Thus HadISST2 and AMIP also differ in the mean at the splice. The 5-GF predicts a dN step of -0.175 W m-2 (single GFs -0.08 to -0.44); with the ice term, -0.156. The pooled real step is -0.23 +/- 0.12 W m-2 (1.5 times). Without the El Chichon months (1982-04 to 1984-12) it is -0.37 +/- 0.12 against a prediction of -0.21 (1.7 times). The residual (real minus prediction) is -0.08 +/- 0.12 and -0.15 +/- 0.12. Thus the real splice response is equal to or up to about two times the GF value. The single pairs scatter widely (-0.77 to +0.13), and in a placebo test with 26 other November dates the residual step is unusual only in IPSL-CM6A-LR (rank 4 of 27) and MPI-ESM1-2-HR (rank 3).

5. **The 2009 Antarctic sea-ice step is reproduced.** Oct-Jan dSW, 2009/10-2013/14 minus 1997/98-2008/09, is -0.19 to -0.73 W m-2 (7 pairs). The albedo-kernel term gives -0.35 to -0.41. This agrees with the kernel-based emulation of sci:sha256:af4b53c1.

6. **1979-2014 radiation trends.** The dataset choice changes the 1979-2014 trend of N by +0.03 to +0.32 W m-2 per decade (without volcanic periods +0.03 to +0.23). The GF plus ice prediction is +0.00 to +0.01 (SST part +0.04 to +0.05, ice part -0.03 to -0.04). Three pairs have clear-sky trend differences that point to forcing differences between the experiment sets (HadGEM3-GC31-LL/LM and -MM -0.14 to -0.15, MPI-ESM1-2-HR +0.12 W m-2 per decade). In the four pairs without them (CNRM-CM6-1, CNRM-CM6-1-HR, GFDL, IPSL; clear-sky trend difference within +/-0.02 without volcanic periods), the dN trend is +0.03 to +0.11 W m-2 per decade. At the 1979-2014 SST trend of 0.085 K per decade, this equals a change of +0.3 to +1.3 W m-2 K-1 in a trend-ratio feedback (AMIPII less negative than HadISST2). The trend estimates have SEs of 0.04-0.07 W m-2 per decade, so single-pair values are uncertain.

## Interpretation

The GF method of the earlier campaign studies predicts the sign of the radiative response to SST-dataset differences, but it under-predicts the size. At annual-to-decadal scales the real response in these seven models is typically 2-3 times the 5-GF value. For the 1981 splice the factor is about 1.5-1.7 but poorly constrained.

Two regional differences explain most of the gap. (1) The models respond more strongly to warm-pool SST than the GFs do. (2) In the models, SST warming at 40-60S increases net downward radiation (less reflection by low cloud in the Southern Ocean and SH subtropics), while most GFs give a small or negative response there. The AMIPII-minus-HadISST2 difference has a large decadal Southern Ocean component (+0.25 K from 1985-1990 to 1994-2008), so this second difference matters for the trend.

Consequences for the earlier campaign numbers:

- The GF-based feedback biases from SST artifacts (for example -0.07 W m-2 K-1 for the 1981 splice in 1979-2014, sci:sha256:36b3c230; the DOISST and OI v2 step effects in sci:sha256:78d7f2e0, sci:sha256:990a6603, sci:sha256:121acf9e, sci:sha256:642d8851) are probably lower bounds in models like these. The ECHAM6 GF, which gave 3-10 times smaller biases than CAM4 (sci:sha256:121acf9e), under-predicts its own model family (MPI-ESM1-2-HR) by 2-4 times here.
- The choice between AMIPII and HadISST2 forcing changes the 1979-2014 radiation trend of real models by about 0.03-0.11 W m-2 per decade where the forcing is clean. The GFs give almost zero for the same SST difference. Thus GF-based studies of dataset dependence of the pattern effect can under-state it.

These results do not show which dataset is correct. They show that the radiative effect of a given SST-dataset difference is larger in these models than linear GFs predict.

## Methods

**Data.** CMIP6 Amon fields ts, rlut, rsut, rlutcs, rsutcs, rsus, rsds, 1979-01 to 2014-12 (GFDL-AM4 amip from 1980-01), from the public Pangeo Google Cloud zarr stores (`files/provenance/cmip6_stores_used.csv` lists every store path and version). Land fraction sftlf from each model (GFDL-CM4C192 has none; we used the PCMDI-AMIP sftof with a one-cell coastal buffer). The GFMIP Jacobians on 5-degree boxes (`gf_boxes.npz`) come from sci:sha256:78d7f2e0 (GFMIP, Zenodo 10414728, and Fredericks et al., Zenodo 18840026; both CC BY 4.0). The 1981 splice map comes from sci:sha256:36b3c230. The CAM5 albedo kernel (Pendergrass et al. 2018, Zenodo 997902) and the PCMDI-AMIP 1.1.9 sftof come from the shared campaign store. Hashes are in `files/provenance/`.

**Reduction** (`11_fetch.py`). Each field is read once from zarr and reduced: area-weighted global mean; area-weighted 5-degree box means (36 x 72); for ts also ocean-only box means (sftlf <= 20%), with ts clamped below at 271.35 K (SST). Nothing raw is kept.

**Series** (`20_series.py`). For each run set: ensemble means; anomalies from the calendar-month means of 1979-2014 (GFDL 1980-2014), computed separately for amip and highresSST-present. N = -(rsut + rlut) (rsdt is common to both runs and cancels). dS = SST(amip) - SST(hSST) on the 24 x 72 GF boxes of 60S-60N. Sea-ice term: CAM5 FSNT albedo kernel (W m-2 per 0.01, monthly) x (alpha_amip - alpha_hSST), alpha = rsus/rsds, ocean boxes poleward of 50 degrees. For MPI-ESM1-2-HR and CNRM-CM6-1-HR (no amip rsus/rsds) we used the mean ice term of the other pairs. The forcing data are the same for all pairs, so this term is nearly model-independent.

**GF test** (`30_validate.py`). Prediction G_k(t) = sum_b Jb_k dS_b(t). Regression dN = c + a G + b I + e, monthly and annual; variants with a linear or cubic time polynomial removed from all series; and without volcanic periods. Trends 1979-2014 by OLS (Newey-West lag 24).

**Control** (`35_full_check.py`). The same regression for each run's own N on the GF prediction from its own SST anomalies, cubic trend removed.

**Steps and epochs** (`40_steps.py`, `45_epochs.py`). Step at 1981-11 by OLS of a level shift, AR(1)-inflated SE; placebo at every November 1984-2009 with the same window lengths. 2009 sea-ice step as in sci:sha256:af4b53c1. Epochs: E0 1979-01 to 1981-10, E1 1985-1990, E2 1994-2008, E3 2009-07 to 2014; volcanic months are in no epoch.

**Regions** (`50_regional.py`). Monthly dN on six area-mean regional dS series and the ice term (Newey-West lag 12). Coefficients are global W m-2 per K of the regional mean. Inverse-variance pooling over pairs.

## Limitations

- **The two experiment sets differ in more than SST and sea ice.** HighResMIP runs start in 1950 and use daily SST; HadGEM3 amip uses forcing index f3 and highresSST-present f1. Clear-sky SW shows a volcanic-aerosol difference in HadGEM3-GC31-LL/LM (+1.2 W m-2 in 1982-84) and clear-sky trend differences in three pairs. We used three defences: removal of time polynomials, exclusion of volcanic periods, and epoch contrasts that avoid volcanic years. The amplification remains in all of them. We cannot exclude other forcing or configuration differences that change in time like the SST difference does. In the four pairs without clear-sky differences the result is the same.
- **Spin-up.** CNRM, HadGEM3, MPI and GFDL amip runs start in 1979-1980. A land or snow spin-up drift could add to the 1980s part of dN. IPSL-CM6A-LR amip runs (20 of 21 members) start in 1958, and IPSL still gives a 3.1 times excess in the decadal contrast.
- **Noise.** Single highresSST-present members carry most of the noise (monthly dN SD 0.4-0.9 W m-2). The 1981 splice test has only 34 months before the splice and is not decisive per pair.
- **Not a GF of the same model.** Only two pairs have a GF of the same model family (ECHAM6, GFDL-AM4), and the GF models are at other resolutions or versions. HadAM3 is an ancestor of HadGEM3, not the same model. The excess may be partly a model-sensitivity difference, but the control (point 1) argues against a general difference.
- **GF domain.** The GFs cover 60S-60N ice-free SST. The sea-ice term is a kernel approximation; its regression coefficient (0.75) and SST near the ice edge are correlated, so the Southern Ocean SST coefficient is less certain than its SE suggests.
- **Which dataset is right is not tested.** HadISST2 also has its own changes (for example at 1981-82). We only measure the response to the difference.
- **Feedback translation.** The trend-ratio values (+0.3 to +1.3 W m-2 K-1) are per K of 60S-60N SST at fixed warming and include forcing-free terms only to the degree that the experiment sets share their forcing.

## Files

- `files/code/`: full pipeline (`run_all.sh`; `get_inputs.sh` fetches the small inputs into the work folder, not into this bundle). Python 3.12 with numpy, scipy, pandas, netCDF4, cftime, matplotlib and numcodecs. The download and reduction take about 2-3 hours with 10 threads; the analysis takes a few minutes.
- `files/results/`: `gf_regression.csv` and `gf_regression_novolc.csv` (all pairs, GFs, time scales, detrending variants), `gf_full_variability.csv` (control), `epochs.csv`, `epoch_contrasts.csv`, `steps_1981_and_2009.csv`, `placebo_1981.csv`, `splice_map_comparison.csv`, `regional_sensitivity.csv`, `regional_sensitivity_pooled.csv`, `trends_1979_2014.csv`, `trends_1979_2014_novolc.csv`, `cmip6_licences.csv`.
- `files/data/pair_series_monthly.csv.gz`: monthly global series per pair (dN, dSW, dLW, clear-sky differences, ice term, dT60, all GF predictions, ensemble-mean N of both runs). `files/data/dsst_boxes_mean.npz`: monthly multi-pair mean dS on the GF boxes and the mean 1981 step map.
- `files/figures/`: Figures 1-4.
- `files/provenance/`: store list with versions, SHA-256 of every reduced field file and of the small inputs.
- `files/NOTICE_external_data.md`: external sources, licences and attribution.

**Reproduce.** Make a work folder W, copy `files/code` to `W/code`, put the shared datasets at `W/../datasets` (or set `SCI_DATASETS`) and the campaign ZIPs at `W/../campaign` (or set `CAMPAIGN`), then run `bash W/code/run_all.sh`. The fetch step is restartable.

## References

- Andrews, T. et al. (2018). Accounting for changing temperature patterns increases historical estimates of climate sensitivity. Geophys. Res. Lett. 45, 8490-8499. doi:10.1029/2018GL078887
- Andrews, T. et al. (2022). On the effect of historical SST patterns on radiative feedback. J. Geophys. Res. Atmos. 127, e2022JD036675. doi:10.1029/2022JD036675
- Bloch-Johnson, J. et al. (2024). The Green's Function Model Intercomparison Project (GFMIP) protocol. J. Adv. Model. Earth Syst. 16, e2023MS003700. doi:10.1029/2023MS003700
- Dong, Y. et al. (2019). Attributing historical and future evolution of radiative feedbacks to regional warming patterns using a Green's function approach. J. Climate 32, 5471-5491. doi:10.1175/JCLI-D-18-0843.1
- Haarsma, R. J. et al. (2016). High Resolution Model Intercomparison Project (HighResMIP v1.0) for CMIP6. Geosci. Model Dev. 9, 4185-4208. doi:10.5194/gmd-9-4185-2016
- Lewis, N. and Mauritsen, T. (2021). Negligible unforced historical pattern effect on climate feedback strength found in HadISST-based AMIP simulations. J. Climate 34, 39-55. doi:10.1175/JCLI-D-19-0941.1
- Pendergrass, A. G., Conley, A. and Vitt, F. M. (2018). Surface and top-of-atmosphere radiative feedback kernels for CESM-CAM5. Earth Syst. Sci. Data 10, 317-324. doi:10.5194/essd-10-317-2018
- Eyring, V. et al. (2016). Overview of the CMIP6 experimental design and organization. Geosci. Model Dev. 9, 1937-1958. doi:10.5194/gmd-9-1937-2016
- Campaign bundles: sci:sha256:36b3c230 (1981 splice), sci:sha256:78d7f2e0 (GF boxes), sci:sha256:af4b53c1 (sea-ice steps), sci:sha256:121acf9e (ECHAM6 GF), sci:sha256:990a6603 (CAM4 GF), sci:sha256:642d8851 (CMIP7Plus forcing), sci:sha256:a44b3670 (ship-buoy adjustment), sci:sha256:dc0ebb92 (CMIP6 pattern comparison).
