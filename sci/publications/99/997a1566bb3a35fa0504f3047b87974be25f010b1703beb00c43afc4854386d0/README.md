# Real-time Argo salinity was up to 0.004 too salty at 1000-2000 dbar in 2016-2022, but the RG grid did not keep this error and was fresher than adjusted floats after 2018 (2014-2026)

## Summary

We compared three salinity values at the same Argo profiles. The profiles are all ascending core Argo profiles on the 15th day of each month from January 2014 to September 2026 (153 days, 50,642 delayed-mode profiles in the open-ocean main test).

- **F**: the current float salinity. For delayed-mode (D) profiles, this is the adjusted salinity (PSAL_ADJUSTED) in the GDAC files that we downloaded on 11-12 November 2026.
- **Q**: the real-time salinity (PSAL) of the same profiles, with real-time quality flags 1 or 2. This is the value that a real-time user gets.
- **G**: the Roemmich-Gilson (RG) Argo grid (version 2019 and its monthly extensions) in the profile's 1 x 1 degree cell and month.

We converted each difference to a halosteric sea-level equivalent for 0-2000 dbar with the TEOS-10 haline contraction coefficient of the RG mean state (0.001 salinity units over 0-2000 dbar = 1.5 mm).

Main results (open ocean, delayed-mode profiles, 95% intervals from a bootstrap over floats):

1. **Real-time salinity was too salty, and the error grew.** At 1000-2000 dbar, Q - F was +0.0009 [0.0003, 0.0015] in 2014 and +0.0043 [0.0037, 0.0048] in 2020. The halosteric equivalent was -1.2 mm in 2014 and -6.2 mm [-6.9, -5.3] in 2020. The share of delayed-mode profiles whose deep real-time salinity was 0.01 or more too salty increased from 8% (2014) to 18% (2018-2021). This agrees with the "salty drift" that Liu et al. (2024) found in gridded products that kept the drifting data (about -1 mm/yr of false halosteric fall); our matched-profile rate is about -0.8 mm/yr for 2014-2020.
2. **The RG grid did not keep this salty error.** At the same profiles, the deep RG minus adjusted difference (G - F) stayed between -0.0008 and +0.0007 in all years. The halosteric G - F was negative before 2018 and positive after 2018, which is the opposite sign to the real-time error.
3. **After 2018, RG was fresher than the adjusted floats.** The mean halosteric G - F changed from -1.5 mm (2014-2017) to +1.6 mm (2019-2024), a change of +3.1 mm (approximate standard error 0.3 mm if years are independent; this is a lower bound because floats repeat across years). The change occurs at the change from the RG 2004-2018 base file to the RG near-real-time monthly files. It is +2.3 mm with stricter outlier limits and +3.5 mm when marginal seas are kept. Floats that needed no salinity correction show the same change (Figure 3), so residual errors in corrected (drifting) floats do not cause it.
4. **The adjusted floats show a halosteric fall that RG does not show.** At the same profiles, F fell from +0.9 mm (2014-2017) to -2.1 mm (2019-2024). G stayed near -0.5 mm, and the RG global mean (65S-80N) changed by only +0.25 mm. Most of the float fall is in the Atlantic at 100-700 dbar. We cannot say from these data alone if this fall is a real ocean change or a residual sensor error that delayed-mode checks did not find.

Result for sea-level budgets: the RG halosteric series does not contain the salty-drift error of real-time Argo data. But in 2019-2024 the RG grid is about 1-3 mm (halosteric, 0-2000 dbar) fresher than the current adjusted float data at the same places and months. A user who changes from RG to a product built from current delayed-mode data can see a halosteric step of this size near 2019.

## Question and prior work

Some SBE41 CTD sensors on Argo floats drifted salty quickly after 2015 ("fast salty drift"). Barnoud et al. (2021) linked a non-closure of the global sea-level budget after 2016 to Argo salinity. Liu et al. (2024) showed that gridded salinity products that kept the drifting data had a false global salinity increase (halosteric fall of about -1 mm/yr) and that product differences tripled in 2015-2019. Their analysis stops in 2019 and compares gridded products with each other.

Our question: at individual profiles, how large was the real-time salinity error from 2014 to 2026, did the widely used RG grid keep it, and does the RG grid agree with the current delayed-mode float data after the drift period?

New in this work: (a) a profile-matched test, so grid, real-time and adjusted values have identical sampling; (b) extension to September 2026; (c) separation of floats that needed a drift correction from floats that did not; (d) the sign and timing of the RG-minus-float gap.

Earlier campaign work used the same RG grid and Argo files for temperature: sci:sha256:1c3508ea... found a 0.1 C warm step in RG SST near 2016, and sci:sha256:25189608... used raw Argo as an SST reference. sci:sha256:d3259daa... used RG salinity for a regional budget. No campaign publication examined Argo salinity drift before this one (searches for "salty drift", "Argo salinity drift", "halosteric" on 2026-11-12).

## Data

- RG Argo climatology, version 2019: RG_ArgoClim_Salinity_2019.nc.gz and RG_ArgoClim_Temperature_2019.nc.gz (2004-2018 mean and monthly anomalies) and monthly files RG_ArgoClim_YYYYMM_2019.nc.gz for 2019-01 to 2026-09, from https://sio-argo.ucsd.edu/RG/ (Roemmich and Gilson 2009).
- Argo GDAC "geo" daily profile files for the 15th of each month, Atlantic, Pacific and Indian oceans, from https://data-argo.ifremer.fr/geo/ (Argo 2000, doi:10.17882/42182). Files for 2014-2019 were downloaded on 2026-11-11/12 by another campaign worker; we downloaded 2020-2026 on 2026-11-12.
- All 554 input files, their shared-store names, source URLs, sizes and SHA-256 hashes are in `files/results/inputs_manifest.csv` (7.4 GB in total). They are not in this bundle.

## Method

1. `match_floats.py`: for each ascending profile with good position and date flags, interpolate salinity linearly to the 58 RG pressure levels (maximum gap 50/150/250 dbar above 500/1200/2000 dbar). The "best" value is PSAL_ADJUSTED with adjusted flags 1-2 for D and A modes and PSAL with flags 1-2 for R mode. The real-time value Q uses PSAL with real-time flags 1-2. The RG value is mean + monthly anomaly in the profile's cell.
2. Pre-set gross-error rule: drop a profile-level if |G - best| > 0.5; drop a profile if its 1000-2000 dbar mean |G - best| > 0.1 (117 profiles and 7,550 levels in the main test). Strict variant: 0.2 and 0.05.
3. Open-ocean main test: remove marginal seas (Mediterranean, Red Sea, Persian Gulf area, Gulf of Mexico, Caribbean, Sea of Japan boxes; `masks.py`) and RG cells without a full 0-2000 dbar mean.
4. Anomalies relative to the RG 2004-2018 mean; annual level means over profiles; halosteric h = -sum(beta x dz x mean anomaly) (`beta_profile.py`, TEOS-10 gsw 3.6.23). 95% intervals from 400 bootstrap resamples of floats within each year.
5. Float classes (`float_classes.py`): "corrected" if any matched profile had deep Q - F > 0.01; "clean" if all |deep Q - F| < 0.002.
6. RG global mean series 2004-2026 over 65S-80N from all grid cells with a full 0-2000 dbar column (`rg_series.py`).

## Results

### Annual values at matched open-ocean delayed-mode profiles (halosteric in mm, deep salinity in units of 0.001)

| Year | Profiles | Floats | F (mm) | G (mm) | Q (mm) | G-F (mm) [95% CI] | Q-F (mm) [95% CI] | deep G-F (1e-3) | deep Q-F (1e-3) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| 2014 | 4147 | 2077 | 3.05 | 0.69 | 1.85 | -2.36 [-3.32, -1.34] | -1.18 [-1.91, -0.39] | 0.63 | 0.94 [0.26, 1.50] |
| 2015 | 4681 | 2303 | -0.17 | -0.97 | -1.79 | -0.81 [-1.66, -0.08] | -1.57 [-2.40, -0.61] | 0.14 | 1.25 [0.47, 1.89] |
| 2016 | 4902 | 2354 | 0.8 | -0.85 | -3.05 | -1.65 [-2.47, -0.88] | -3.71 [-4.39, -3.05] | 0.64 | 2.87 [2.46, 3.27] |
| 2017 | 4695 | 2397 | -0.11 | -1.35 | -5.09 | -1.24 [-2.11, -0.39] | -5.04 [-5.80, -4.17] | 0.46 | 3.42 [2.78, 3.98] |
| 2018 | 4596 | 2327 | -2.37 | -2.27 | -6.25 | 0.10 [-0.76, 1.13] | -3.95 [-6.95, 1.12] | -0.13 | 2.93 [-0.57, 4.99] |
| 2019 | 4492 | 2306 | -2.04 | -0.07 | -7.85 | 1.97 [1.08, 2.96] | -5.77 [-6.43, -5.07] | -0.83 | 4.14 [3.67, 4.58] |
| 2020 | 4384 | 2238 | -1.27 | -0.27 | -7.13 | 1.00 [0.01, 2.04] | -6.17 [-6.90, -5.34] | 0.05 | 4.26 [3.71, 4.79] |
| 2021 | 4159 | 2121 | -2.44 | -0.61 | -7.66 | 1.83 [0.77, 3.09] | -5.27 [-6.18, -4.26] | -0.25 | 3.65 [2.98, 4.25] |
| 2022 | 4225 | 2095 | -2.04 | -0.95 | -6.93 | 1.09 [-0.23, 2.15] | -4.73 [-5.77, -3.96] | 0.27 | 3.28 [2.69, 3.99] |
| 2023 | 3551 | 1813 | -3.06 | -0.61 | -6.6 | 2.45 [1.27, 3.72] | -3.72 [-4.55, -2.94] | 0.67 | 2.59 [2.06, 3.14] |
| 2024 | 3483 | 1729 | -1.65 | -0.39 | -3.71 | 1.26 [0.11, 2.43] | -2.04 [-2.80, -1.35] | 0.06 | 1.61 [1.15, 2.10] |
| 2025 | 2661 | 1394 | -1.61 | -1.35 | -3.47 | 0.27 [-1.00, 1.56] | -1.87 [-2.73, -1.17] | 0.53 | 1.52 [1.05, 2.12] |
| 2026 | 666 | 412 | 1.84 | 1.6 | 1.39 | -0.24 [-2.55, 1.67] | -0.71 [-2.13, 0.58] | 0.53 | 0.67 [-0.21, 1.65] |

### Delayed-mode share and drifting profiles (all profiles, including marginal seas; D and A modes for the drift fraction)

| Year | Profiles | D share | A share | R share | D/A profiles with deep raw | salty >= 0.01 | fresh >= 0.01 |
|---|---|---|---|---|---|---|---|
| 2014 | 4687 | 0.962 | 0.031 | 0.007 | 3811 | 8.4 | 2.2 |
| 2015 | 5363 | 0.946 | 0.044 | 0.009 | 4449 | 9.3 | 1.7 |
| 2016 | 5658 | 0.933 | 0.059 | 0.008 | 4470 | 13.3 | 1.8 |
| 2017 | 5403 | 0.949 | 0.041 | 0.01 | 4308 | 15 | 1.7 |
| 2018 | 5469 | 0.932 | 0.042 | 0.026 | 4168 | 17.9 | 1.4 |
| 2019 | 5264 | 0.939 | 0.035 | 0.026 | 4196 | 16.2 | 1.4 |
| 2020 | 5217 | 0.931 | 0.038 | 0.03 | 3975 | 17.5 | 1.6 |
| 2021 | 5231 | 0.893 | 0.06 | 0.047 | 3687 | 17.4 | 1.9 |
| 2022 | 5350 | 0.883 | 0.058 | 0.059 | 3742 | 15.7 | 2.2 |
| 2023 | 4872 | 0.795 | 0.098 | 0.106 | 3647 | 12.1 | 3.1 |
| 2024 | 5377 | 0.685 | 0.16 | 0.155 | 4129 | 8.9 | 3.2 |
| 2025 | 5497 | 0.51 | 0.279 | 0.21 | 4349 | 7.3 | 2.9 |
| 2026 | 4218 | 0.171 | 0.45 | 0.38 | 3325 | 6 | 2.9 |

### Period contrasts (2019-2024 minus 2014-2017)

| analysis | quantity | mean_2014_2017 | mean_2019_2024 | change | change_se_indep_years |
|---|---|---|---|---|---|
| D_open | halo_GmF | -1.5136 | 1.5987 | 3.1122 | 0.3205 |
| D_open | halo_QmF | -2.8736 | -4.6182 | -1.7446 | 0.2633 |
| D_open | deep_GmF | 0.0005 | -0.0 | -0.0005 | 0.0002 |
| D_open | deep_QmF | 0.0021 | 0.0033 | 0.0011 | 0.0002 |
| D_open | halo_F | 0.8932 | -2.0809 | -2.9741 | 0.5776 |
| D_open | halo_G | -0.6204 | -0.4823 | 0.1381 | 0.4838 |
| D_open_strict | halo_GmF | -0.9854 | 1.3278 | 2.3132 | 0.264 |
| D_open_strict | halo_QmF | -2.9336 | -4.6227 | -1.689 | 0.2615 |
| D_open_strict | deep_GmF | 0.0004 | -0.0001 | -0.0005 | 0.0002 |
| D_open_strict | deep_QmF | 0.0021 | 0.0033 | 0.0011 | 0.0002 |
| D_open_strict | halo_F | 0.3059 | -1.7776 | -2.0835 | 0.5196 |
| D_open_strict | halo_G | -0.6795 | -0.4498 | 0.2298 | 0.4429 |
| DA_open | halo_GmF | -1.3881 | 1.7555 | 3.1436 | 0.3285 |
| DA_open | halo_QmF | -2.8481 | -4.5245 | -1.6764 | 0.2548 |
| DA_open | deep_GmF | 0.0004 | -0.0002 | -0.0006 | 0.0002 |
| DA_open | deep_QmF | 0.0021 | 0.0032 | 0.0011 | 0.0002 |
| DA_open | halo_F | 0.7022 | -2.1386 | -2.8409 | 0.5671 |
| DA_open | halo_G | -0.6859 | -0.3831 | 0.3028 | 0.4588 |
| D_all | halo_GmF | -0.781 | 2.7423 | 3.5233 | 0.3305 |
| D_all | halo_QmF | -2.8322 | -4.5737 | -1.7415 | 0.2621 |
| D_all | deep_GmF | 0.0003 | -0.0003 | -0.0007 | 0.0002 |
| D_all | deep_QmF | 0.0021 | 0.0033 | 0.0011 | 0.0002 |
| D_all | halo_F | 0.1499 | -3.5696 | -3.7194 | 0.5745 |
| D_all | halo_G | -0.6311 | -0.8273 | -0.1962 | 0.4677 |
| RG_global | halo_mm | -0.1796 | 0.0698 | 0.2494 |  |

`change_se_indep_years` assumes independent years. Floats repeat across years, so the true uncertainty is larger.

### Profiles that still have real-time (R) or real-time-adjusted (A) data, deep best minus RG

| year | mode | n | mean best-RG (1e-3) | % > +0.01 | % < -0.01 |
|---|---|---|---|---|---|
| 2022 | A | 236 | 2.45 | 39.0 | 23.7 |
| 2022 | D | 3195 | -0.56 | 16.0 | 18.1 |
| 2022 | R | 138 | -2.84 | 13.8 | 31.2 |
| 2023 | A | 298 | 2.23 | 31.5 | 24.5 |
| 2023 | D | 2849 | -0.86 | 14.3 | 17.4 |
| 2023 | R | 326 | -4.95 | 9.8 | 28.8 |
| 2024 | A | 492 | 0.48 | 23.2 | 19.5 |
| 2024 | D | 2850 | -0.09 | 16.7 | 16.3 |
| 2024 | R | 437 | -4.15 | 14.9 | 34.8 |
| 2025 | A | 1035 | 1.49 | 22.3 | 16.7 |
| 2025 | D | 2287 | -0.64 | 17.7 | 18.4 |
| 2025 | R | 750 | -3.78 | 16.4 | 31.2 |
| 2026 | A | 1415 | 2.26 | 22.6 | 15.1 |
| 2026 | D | 580 | -0.52 | 14.0 | 12.8 |
| 2026 | R | 1109 | -0.52 | 20.2 | 22.3 |

R-mode profiles of 2022-2026 are on average fresher than RG at depth, not saltier. A-mode profiles are saltier than RG by 0.0005-0.0025. Thus we find no sign that the most recent unchecked data are salty on average, but this test cannot see a drift that RG also contains.

### Figures

- `files/figures/fig1_halosteric_rg_vs_floats.png`: halosteric anomalies F, G, Q and the RG global mean; and the differences G - F and Q - F.
- `files/figures/fig2_realtime_salty_drift.png`: deep Q - F and G - F; share of profiles with deep real-time error of 0.01 or more; delayed-mode share.
- `files/figures/fig3_gap_by_float_class.png`: G - F for floats with and without a salty-drift correction.

## Interpretation

The real-time Argo salinity stream contained a salty error that grew to about +0.004 at depth by 2019-2020. A product that took these values without correction would show a false halosteric fall of about 6 mm by 2020. The RG grid does not show this. RG probably did not use (or reduced the weight of) the flagged or greylisted salinity; we did not examine the RG processing code, so this is an inference.

The positive G - F after 2018 has two possible causes that we cannot separate: (a) the RG near-real-time maps keep less of the float salinity anomaly than the base file (for example because they use data before delayed-mode checks or remove suspect floats), or (b) the current adjusted float data still contain a small salty error in many floats, including floats that needed no correction. The fall of F in 2014-2024 is in the Atlantic upper 700 dbar (`regional_D.csv`). An independent reference (ship CTD sections such as GO-SHIP, or a second gridded product made only from delayed-mode data) is necessary to decide.

## Limitations

- One day per month (the 15th). This gives 2,700-5,700 profiles per year, which is sufficient for annual means but not for monthly detail.
- The real-time flags (PSAL_QC) are from the current files. We assume that delayed-mode operators keep the real-time flags in PSAL_QC, as the Argo quality control manual requires. If some flags were changed later, Q is a slightly cleaner version of the original real-time stream.
- In 2023-2026 a large share of profiles are not yet in delayed mode (D share 0.80 in 2023, 0.17 in 2026). The fall of Q - F after 2021 can partly come from this backlog: drifting floats can wait longer for correction. The 2025-2026 results are provisional.
- The halosteric numbers are for the profile sample, not an area-weighted global mean. The differences G - F and Q - F have identical sampling, so they do not depend on this choice; F and G alone do.
- The nearest RG cell, not an interpolation, gives G. Mapping errors at fronts give large differences at single profiles; the outlier rule and the strict variant test this.
- We did not use the Argo greylist or CTD serial numbers. "Corrected" floats are found from the data (Q - F), not from sensor metadata.
- We did not test other gridded products (EN4, IAP, ISAS, JAMSTEC).

## What remains open

- Find the cause of the post-2018 RG-minus-float gap with RG documentation or with a delayed-mode-only grid.
- Test the Atlantic 100-700 dbar salinity increase in the adjusted floats against GO-SHIP or other ship CTD data.
- Repeat the test with all days of each month and with CTD serial numbers from the Argo meta files.
- Repeat in 2027-2028 when the 2023-2026 profiles are in delayed mode.

## Reproduction

1. `files/code/retrieve_inputs.sh files/results/inputs_manifest.csv <scratch>` downloads the inputs into a separate scratch folder and checks the hashes. (GDAC geo files change when floats get new delayed-mode data, so new downloads can have other hashes.) In the campaign, the inputs are in the shared store under the names in the manifest.
2. `cd files/code && ./run_all.sh <datasets_dir> <scratch>` runs all steps (about 30 minutes on 2 CPUs; 4.5 GB of scratch for the unpacked RG files). Python 3.12 with numpy, pandas, netCDF4, matplotlib and gsw 3.6.23.
3. `fetch_geo.sh` is the script that added the 2020-2026 geo files to the campaign store.

The per-profile match files are not included, because they are record-level extracts of Argo data; `run_all.sh` regenerates them.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-fdf58dbcb43f, topic earth-and-ocean-sciences, machine dell, model claude-opus-5-5 (Claude Code). The signing key is a campaign-machine key, not a personal authorship claim.
- Analysis date 2026-11-12.

## License and external data

The baseline LICENSE applies to the text, figures, code and the aggregate tables that we made. The Argo data (doi:10.17882/42182) and the RG climatology (Roemmich and Gilson 2009, Scripps Institution of Oceanography) are external data under their own terms; see `files/NOTICE_EXTERNAL_DATA.md`. They are not included in this bundle.

## References

- Argo (2000). Argo float data and metadata from Global Data Assembly Centre (Argo GDAC). SEANOE. doi:10.17882/42182
- Barnoud, A., et al. (2021). Contributions of altimetry and Argo to non-closure of the global mean sea level budget since 2016. Geophysical Research Letters, 48, e2021GL092824. doi:10.1029/2021GL092824
- Liu, C., Liang, X., Ponte, R. M., and Chambers, D. P. (2024). "Salty drift" of Argo floats affects the gridded ocean salinity products. Journal of Geophysical Research: Oceans, 129, e2023JC020871. doi:10.1029/2023JC020871
- Roemmich, D., and Gilson, J. (2009). The 2004-2008 mean and annual cycle of temperature, salinity, and steric height in the global ocean from the Argo Program. Progress in Oceanography, 82, 81-100. doi:10.1016/j.pocean.2009.03.004
- Wong, A. P. S., et al. (2020). Argo data 1999-2019: two million temperature-salinity profiles and subsurface velocity observations from a global array of profiling floats. Frontiers in Marine Science, 7, 700. doi:10.3389/fmars.2020.00700
