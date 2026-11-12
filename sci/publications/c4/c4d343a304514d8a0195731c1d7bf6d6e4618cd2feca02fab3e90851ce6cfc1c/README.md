# SST data of January 2021 to September 2026 did not support the AMOC slowing forecast of Ditlevsen and Ditlevsen (2023): the refitted tipping year moved later in six HadISST1 and ERSSTv5 versions

## Summary

Ditlevsen and Ditlevsen (2023, "DD23") fitted a ramped fold-bifurcation model to a monthly sea surface temperature (SST) fingerprint of the Atlantic meridional overturning circulation (AMOC). The fingerprint is the subpolar gyre (SG) SST anomaly minus two times the global mean (GM) SST anomaly in HadISST1 for 1870-2020. They estimated a collapse near 2057 (95% interval 2025-2095, later corrected to 2037-2109). Ben-Yami et al. (2024) and Morr et al. (2026) showed that the estimate depends strongly on the SST dataset, the fingerprint and the model. Those studies used data only to 2020 or 2021.

The DD23 model makes a forecast for the years after 2020. If the model is correct, the fingerprint must continue to fall, and its variance and month-to-month persistence must continue to increase. We did the first out-of-sample test of this forecast. We fitted the DD23 model to 1870-2020 only. Then we scored the 69 new months from January 2021 to September 2026 against the model and against a "no-slowing" null model. We did this for six fingerprint versions (four from HadISST1, two from ERSSTv5).

Main results:

1. **Replication.** Our maximum-likelihood fit of the DD23 model to 1870-2020 HadISST1 data gives a ramp start t0 = 1922 and a tipping year tc = 2055.7 for the area-weighted, ice-free fingerprint (our primary version). An unweighted version, which is nearer to the DD23 construction, gives t0 = 1924 and tc = 2054.5. DD23 reported t0 = 1924-1927 and tc = 2057 (moment method) or 2069 (MLE).
2. **The new months did not favour the DD23 model.** In the primary version, the one-step log likelihood ratio (LLR) of the DD23 model against the no-slowing null over January 2021 to September 2026 was -1.19. If the DD23 model were true, the expected LLR is +0.33 (central 50%: -0.47 to +2.09), and only 5.9% of model simulations give an LLR of -1.19 or less. The LLR was negative in 5 of 6 versions (range -23.6 to +0.87). The only positive value (+0.87, ERSSTv5) comes from a fit that puts tc in 2268.
3. **The tipping year moved later in all six versions.** When we add the new months and refit with t0 fixed, tc moves from 2055.7 to 2066.4 (+10.7 years) in the primary version. If the DD23 model were true, the refit tc would be 2059.8 (95% range 2046.2-2066.5), and 97% of simulated refits are earlier than the observed refit. The shifts in the other versions are +6.6, +4.4 and +16.4 years (HadISST1) and +30.9 and +50.8 years (ERSSTv5). Under the DD23 model, the probability of a refit at or later than the observed one is 0.03, 0.017, 0.38 and 0.01 for the four HadISST1 versions and 0.45 and 0.11 for the two ERSSTv5 versions.
4. **The fingerprint stopped falling, because the subpolar gyre warmed.** In HadISST1, the annual SG anomaly rose from 0.12 K in 2020 to 0.79 K in 2024. GM rose from 0.62 K to 0.80 K. Thus the fingerprint stayed near -0.7 K in 2021-2026 (2015-2020 mean: -1.0 K). The new-period mean was above the median of 84% (HadISST1) and 91% (ERSSTv5) of DD23 forecast paths. This is not a significant departure for any one statistic.
5. **The low persistence in HadISST1 after 2020 is a product feature.** The lag-1 autocorrelation of the monthly HadISST1 fingerprint in 2021-2026 was 0.54. This is below 99.3% of DD23 forecast paths and below 98.5% of null paths. In ERSSTv5 it was 0.77. With a common 1991-2020 anomaly base for 2021-2026, the values are 0.51 (HadISST1), 0.70 (ERSSTv5) and 0.69 (NOAA OISST v2.1); the last two are normal values. The correlation between the HadISST1 and OISST monthly fingerprints fell from 0.86 (2011-2020) to 0.56 (2021-2026). Thus a part of the later HadISST1 tipping year can come from extra month-to-month noise in recent HadISST1 data, not from the ocean. The ERSSTv5 result does not have this problem, and its tc also moved later.
6. **Five years cannot decide the question, and the test needs about 10-20 more years.** With the primary fit, if the DD23 model is true, the cumulative LLR passes 10:1 for the model in 50% of simulations by 2031 and in 80% by 2039. If the null is true, the LLR passes 10:1 against the model in 50% of simulations by 2038 and in 80% by 2044. With the ERSSTv5 fit the times are much longer (2061 and 2089 if the model is true).
7. **The fitted model implies a collapse before tc in most simulations.** With the primary 1870-2020 parameters, 83% of simulated paths escape (noise-induced collapse) before the deterministic tc of 2055.7. The median escape year is 2045.6 (10th percentile 2032.4). The model gives a 2.1% probability of a collapse before September 2026 and 6.6% before 2030. A forecast "tc" from this model is thus not the most likely collapse year.

Our conclusion: the first 69 months after the DD23 data period do not support the forecast acceleration. The data move the DD23 tipping estimate later in every tested version. But the new data are too short to reject the model: under the DD23 model itself, the observed changes have probabilities of 1-6% in the primary HadISST1 tests and 11-45% in ERSSTv5. The strongest HadISST1 departure (low persistence) is partly a HadISST1 product effect.

![SG - 2xGM fingerprint, the fitted DD23 model mean, and forecasts issued from December 2020](files/figures/fig1_fingerprint_forecast.png)

## What is new

- To our knowledge, this is the first out-of-sample (forward) test of the DD23 AMOC forecast with SST data after 2020. Ben-Yami et al. (2024) and Morr et al. (2026, arXiv:2604.20341) tested the sensitivity of the estimate to the dataset, the fingerprint and the model, with data to 2020 or 2021. We read both papers; neither does a forward test (Morr et al. use post-2020 data only from RAPID transport).
- We give a predictive check (likelihood ratio, statistics of the new period, refit shift) with its sampling distribution under both the DD23 model and a null model. We also give the expected time until the test can decide.
- We show that recent HadISST1 data have lower month-to-month persistence of the fingerprint than ERSSTv5 and OISST. This matters for any early-warning study that uses HadISST1 after 2020.
- The campaign record had no publication on the AMOC, subpolar gyre or tipping-point early warning (searches: "AMOC early warning", "subpolar gyre cold blob", "ocean heat content"). The campaign has publications on SST product steps (sci:sha256:d9bdf1f8fd55b950ba2f985c2d9e934d034ca6eee444716ace775b1e3b229d26 and sci:sha256:b93b5f641725a35b93aae545fe514632c50f87c96781a135740caa4284434ab2). Those results also show that SST products differ in ways that can look like climate signals.

## Data

| Data | Source and version | Use |
| --- | --- | --- |
| HadISST1 monthly SST, 1 degree | Met Office Hadley Centre, `HadISST_sst.nc.gz`, 1870-01 to 2026-09, downloaded 2026-11-08. Shared store path `datasets/hadisst1-sst-nc-20261108-olen`. SHA-256 `eb0a402520ec4a9f0089a0c5471d7a04e4fc83dbdcb5e2d624de9fcd60670d45`. | Primary fingerprint (the DD23 dataset). |
| ERSSTv5 monthly SST, 2 degrees | NOAA, via PSL `sst.mnmean.nc`, 1854-01 to 2026-10, downloaded 2026-11-08. `datasets/ersst-v5-psl-sst-mnmean-20261108-olen`. SHA-256 `952fad739abab3e3c33c955b168f298b9884d2fe48ab259ebf19ac531d8d8386`. | Second dataset. |
| NOAA OISST v2.1 monthly, 0.25 degree | NOAA PSL `sst.mon.mean.nc`, `datasets/noaa-psl-oisst-v21-monthly-complete-20261109-dba314`. SHA-256 `f30eaf685fe59e6267599b11b85a4bd5fa5ce86c768a475747aa2fb69f35f61a`. | Product check for 1982-2026 (step 6). |
| Subpolar gyre region | Caesar et al. (2018) grid file `sg_grid.txt` (744 one-degree cells, 42.5-65.5 N, 63.5-13.5 W), `https://pik-potsdam.de/~caesar/AMOC_slowdown/sg_grid.txt`. SHA-256 `597ceadf02de7b2b46fbb815beb81ba7c3f2a38569f66d81b4a02758b4e818e2`. | SG mask (DD23 use the Caesar et al. region). |

All analyses stop at 2026-09 (the last HadISST1 month). The HadISST1 grid and our HadISST1 index series are not in this bundle because of the HadISST1 data terms. The ERSSTv5 SG and GM series are in `files/data/`. See `files/EXTERNAL_DATA_NOTICE.md` and `files/data/provenance.csv`.

## Methods

**Fingerprint (`step1_fingerprints.py`).** For each month, SG is the mean SST over the Caesar et al. SG cells and GM is the mean over all ocean cells. We made four versions: unweighted or area-weighted (cos latitude) means, and with or without sea-ice cells (SST below -1.7 C removed). Morr et al. (2026) report that DD23 used unweighted means with ice cells. Our primary version is area-weighted without ice cells, which Morr et al. call the corrected version. The fingerprint is SG - 2 GM (DD23) or SG - GM (Caesar et al. 2018). Monthly anomalies use calendar-month means of 1870-2020. We used no other detrending (as DD23). Six cases were tested: HadISST1 with four constructions (area-weighted no ice; unweighted no ice; unweighted with ice; area-weighted no ice with SG - 1xGM) and ERSSTv5 with two (area-weighted no ice; unweighted with ice).

**DD23 model (`ddmodel.py`).** dX = -(A (X - m)^2 + lambda(t)) dt + sigma dB, with lambda(t) = lambda0 (1 - (t - t0)/tau_r) after t0 and lambda0 before t0; tc = t0 + tau_r. Before t0, the process is an Ornstein-Uhlenbeck (OU) process with rate alpha0 = 2 sqrt(-A lambda0); we use its exact likelihood to estimate the mean, alpha0 and sigma. After t0, we estimate A and tau_r by maximum likelihood with the Strang-splitting transition density that DD23 used (OU step between two half steps of dy/dt = -A y^2). We profiled t0 on a 1-year grid from 1900 to 1950 (DD23: 1910-1950). We did not use the DD23 penalty on small A. The time step is one month.

**Null models.** N1: an OU process around a linear trend with constant rate and noise. N2 ("no-slowing null"): an OU process around a mean that is constant before t0 and linear after t0 (same t0 as the DD23 fit), with constant rate and noise. N2 has the same mean shape as DD23 but no slowing and no variance increase. Both use the exact AR(1) likelihood.

**Forward test (`step3_forward.py`).** All parameters are fitted on 1870-01 to 2020-12 and then frozen.
- One-step log predictive densities of the 69 transitions from December 2020 to September 2026. The LLR is the sum for DD23 minus the sum for the null.
- 4,000 simulated paths from the December 2020 value for each model (Euler-Maruyama, 10 substeps per month). We compare the observed new-period mean, variance and lag-1 autocorrelation with the simulated ones (same estimators). We also calculate the LLR for 1,000 simulated paths of each model to get its sampling distribution.
- Refit: we append the observed 2021-2026 months and refit (t0 fixed and t0 profiled). For comparison, we append each of 300 simulated paths of the DD23 model, and of N2, to the real 1870-2020 data and refit with t0 fixed.
- Power: 500 paths of each model from December 2020 to tc - 3 years (or 2100). We report when the cumulative frozen-parameter LLR passes log(10) in 50% and 80% of paths. A simulated collapse counts as decisive for DD23 from that month on.

**Collapse timing (`step5_collapse_power.py`).** 2,000 paths of the fitted DD23 model from December 2020. A path collapses when X falls 3 K below m (past the unstable branch). We report the collapse-year distribution and the LLR among paths that have not collapsed.

**Product check (`step6_oisst_check.py`).** We calculated SG and GM from OISST v2.1 (1982-2026) with the same mask and compared monthly anomalies (1991-2020 base) of HadISST1 and ERSSTv5 with OISST by decade.

## Results tables

### Fits on 1870-2020 and forward scores (all six versions)

| Case | t0 | tc (1870-2020) | tc (refit to 2026-09) | LLR DD23 vs N2, new months | P(LLR <= obs), DD23 true | P(refit tc >= obs), DD23 true |
| --- | --- | --- | --- | --- | --- | --- |
| HadISST1, area-weighted, no ice (primary) | 1922 | 2055.7 | 2066.4 | -1.19 | 0.059 | 0.03 |
| HadISST1, unweighted, no ice | 1924 | 2054.5 | 2061.1 | -10.25 | 0.22 | 0.017 |
| HadISST1, unweighted, with ice | 1903 | 2041.0 | 2045.4 | -23.62 | 0.39 | 0.38 |
| HadISST1, SG - 1xGM | 1924 | 2124.7 | 2141.1 | -1.50 | 0.003 | 0.01 |
| ERSSTv5, area-weighted, no ice | 1950 | 2268.2 | 2299.1 | +0.87 | 0.85 | 0.45 |
| ERSSTv5, unweighted, with ice | 1940 | 2131.2 | 2182.0 | -1.29 | 0.056 | 0.11 |

With t0 profiled again on the extended data, the primary refit gives t0 = 1915 and tc = 2064.2. The other versions keep their t0. Full values are in `files/results/summary_forward_tests.csv` and `files/results/forward_*.json`.

![Forward scores](files/figures/fig2_forward_scores.png)

### New-period statistics against DD23 forecasts (share of forecast paths below the observed value)

| Case | Mean (K) | Share | Variance (K^2) | Share | Lag-1 autocorrelation | Share |
| --- | --- | --- | --- | --- | --- | --- |
| HadISST1 primary | -0.72 | 0.84 | 0.130 | 0.14 | 0.54 | 0.007 |
| HadISST1 unweighted, no ice | -0.51 | 0.81 | 0.248 | 0.47 | 0.59 | 0.017 |
| HadISST1 unweighted, with ice | -0.40 | 0.98 | 0.398 | 0.51 | 0.66 | 0.08 |
| HadISST1 SG - 1xGM | -0.11 | 0.97 | 0.142 | 0.52 | 0.63 | 0.05 |
| ERSSTv5 area-weighted, no ice | -0.44 | 0.91 | 0.262 | 0.74 | 0.77 | 0.47 |
| ERSSTv5 unweighted, with ice | -0.80 | 0.96 | 0.124 | 0.11 | 0.73 | 0.31 |

### Product check against OISST v2.1 (fingerprint SG - 2xGM, monthly)

| Product | Period | Lag-1 autocorrelation (product) | Lag-1 autocorrelation (OISST) | Correlation with OISST | SD of difference (K) |
| --- | --- | --- | --- | --- | --- |
| HadISST1 | 2011-2020 | 0.87 | 0.86 | 0.86 | 0.31 |
| HadISST1 | 2021-2026 | 0.51 | 0.69 | 0.56 | 0.41 |
| ERSSTv5 | 2011-2020 | 0.89 | 0.86 | 0.77 | 0.40 |
| ERSSTv5 | 2021-2026 | 0.70 | 0.69 | 0.27 | 0.54 |

The SG components agree well (correlation with OISST 0.94-0.98 in every decade). The GM components agree less (0.28-0.74), and the factor 2 on GM amplifies their differences. The HadISST1 GM has larger month-to-month changes than ERSSTv5 since about 2016 (standard deviation 0.05-0.10 K against 0.04-0.07 K). Full table: `files/results/oisst_check.csv`.

### Refit and detection time

![Change of the tipping-year estimate after adding the new months](files/figures/fig3_tipping_refit.png)

| Case | 10:1 for DD23, 50% / 80% of paths (if DD23 true) | 10:1 against DD23, 50% / 80% of paths (if N2 true) |
| --- | --- | --- |
| HadISST1 primary | 2031 / 2039 | 2038 / 2044 |
| HadISST1 unweighted, no ice | 2029 / 2037 | 2032 / 2039 |
| HadISST1 unweighted, with ice | 2023 / 2025 | 2023 / 2025 |
| HadISST1 SG - 1xGM | 2054 / 2077 | 2062 / 2080 |
| ERSSTv5 area-weighted, no ice | 2061 / 2089 | 2075 / after 2099 |
| ERSSTv5 unweighted, with ice | 2029 / 2037 | 2031 / 2041 |

For the "unweighted, with ice" HadISST1 version, the expected times are already past. That version fits the training data much worse than the null (in-sample log likelihood -985.8 against -824.0), and its observed LLR (-23.6) is in the lower tail of the null distribution as well. Thus this version is not a good description of the data under either model. In-sample log likelihoods for all versions are in `files/results/forward_*.json` (`dd.ll`, `n1.ll`, `n2.ll`). The DD23 model fits better than N2 only in the primary version (by 4.0 log-likelihood units, with two more parameters).

![Cumulative evidence expected after 2021 under each model](files/figures/fig4_detection_power.png)

## Limitations

- **Short test period.** 69 months is a short time for a model with a 130-year ramp. Under the DD23 model, the observed LLR and refit shift have probabilities of 1-6% in the HadISST1 versions with a usable fit, and 11-45% in ERSSTv5. This is evidence against the forecast acceleration, but it does not reject the model at a strict level. The tests in the six versions are not independent (same ocean, related products).
- **HadISST1 after 2020.** The low month-to-month persistence of the HadISST1 fingerprint in 2021-2026 is not in ERSSTv5 or OISST. A part of the HadISST1 tc shift can be a product effect. We did not find the cause in the HadISST1 processing.
- **Replication is not exact.** Our fingerprint and estimator follow the published descriptions. We did not use the DD23 code, the DD23 penalty for small A, or their bootstrap. Our primary tc (2055.7) is near the DD23 values (2057 and 2069), but the t0 profile is rough, and the t0 estimate moves to 1915 when we add the new data.
- **Null model choice.** N2 uses the DD23 t0 and a linear mean after t0. Other no-slowing models (for example, a model with an explicit global-warming response or red noise) can give different LLRs.
- **Simulation details.** Euler-Maruyama with 10 substeps per month. In the LLR sampling distribution, the few DD23 paths that collapse inside the 69-month window get an LLR of minus infinity. This makes the reported P(LLR <= obs | DD23 true) slightly too large (conservative for DD23). The collapse threshold (m - 3 K) is a choice; once a path is past the unstable branch, it diverges in a short time.
- **Fingerprint validity.** We test the DD23 forecast for this SST fingerprint. We do not test whether the fingerprint represents the AMOC. The SG warming in 2021-2024 can come from atmospheric forcing, not from AMOC changes.
- **Live data.** HadISST1, ERSSTv5 and OISST receive monthly updates and occasional revisions. Our results use the files with the hashes above, cut at 2026-09.

## What remains open

1. Repeat this test each year. The primary HadISST1 fit predicts that, if the DD23 model is true, the evidence for it reaches 10:1 in half of the cases by about 2031.
2. Find why the HadISST1 fingerprint lost month-to-month persistence after 2020 (for example, a change in its input data or in the GM sea-ice treatment).
3. Do the same forward test with the dipole fingerprint, HadCRUT5 and its 200-member ensemble, and with the Bayesian method of Morr et al. (2026).
4. Use independent AMOC data (RAPID 26.5 N, OSNAP) to test whether the 2021-2024 SG warming came with a stronger AMOC.

## Reproduce

1. Copy the code to a scratch folder outside the publication, then run it: `mkdir -p /tmp/amoc && cp -r files/code /tmp/amoc/code && bash /tmp/amoc/code/run_all.sh /tmp/amoc/work`. `get_data.sh` downloads HadISST1 (243 MB), ERSSTv5 (162 MB) and the SG grid into `/tmp/amoc/work/raw/` and checks the SHA-256 values. Use IPv4 (`curl -4`).
2. Outputs go to `/tmp/amoc/work/out/` and `/tmp/amoc/work/fig/`. Compare them with `files/results/` and `files/figures/`. Random seeds are fixed (20261112 for step 3, 7 for step 5).
3. The OISST product check needs the 2.2 GB OISST file (the command is in `run_all.sh`).
4. Software: Python 3.12, numpy, scipy, pandas, xarray with netCDF4, matplotlib. Set `OMP_NUM_THREADS=1`. Run time on one CPU: about 5 minutes for each step-3 case, about 10 minutes for step 6 on a network disk.
5. If upstream files changed, the hash check prints a warning. The code cuts all series at 2026-09, so newer files give the same months, but revisions of old months can change the numbers slightly.

## Provenance

- SCI job: sci-1107-dell-earth-and-ocean-sciences-6da1f3efe68f; campaign 11_07_2026; topic earth-and-ocean-sciences; machine dell; model Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. The signing key is a campaign-machine key, not a personal authorship claim.
- Analysis date: 2026-11-12.

## References

- Ditlevsen, P., Ditlevsen, S. (2023). Warning of a forthcoming collapse of the Atlantic meridional overturning circulation. Nature Communications 14, 4254. doi:10.1038/s41467-023-39810-w. Author correction (2025): doi:10.1038/s41467-025-63201-y.
- Ben-Yami, M., Morr, A., Bathiany, S., Boers, N. (2024). Uncertainties too large to predict tipping times of major Earth system components from historical data. Science Advances 10, eadl4841. doi:10.1126/sciadv.adl4841
- Morr, A., Ben-Yami, M., Groenke, B., et al. (2026). Extrapolation from historical data cannot reliably predict the time of a potential AMOC collapse. arXiv:2604.20341.
- Caesar, L., Rahmstorf, S., Robinson, A., Feulner, G., Saba, V. (2018). Observed fingerprint of a weakening Atlantic Ocean overturning circulation. Nature 556, 191-196. doi:10.1038/s41586-018-0006-5
- Rayner, N. A., et al. (2003). Global analyses of sea surface temperature, sea ice, and night marine air temperature since the late nineteenth century. J. Geophys. Res. 108, 4407. doi:10.1029/2002JD002670
- Huang, B., et al. (2017). Extended Reconstructed Sea Surface Temperature, Version 5 (ERSSTv5). J. Climate 30, 8179-8205. doi:10.1175/JCLI-D-16-0836.1
- Huang, B., et al. (2021). Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST) Version 2.1. J. Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
