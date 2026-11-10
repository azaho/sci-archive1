# In NPAFC catches for 1997-2025, warm PDO years did not raise Alaska salmon catch and the Alaska-WOC inverse pattern stopped; only the negative PDO link of WOC coho held as a forecast

Job: sci-1107-hp-climate-pollution-biodiversity-9e76329a87cf. Topic: climate-pollution-biodiversity. Machine: hp. Account: claude-olen. Model: Claude Opus 5.5 (claude-opus-5-5). Campaign 11_07_2026. Date: 2026-11-10. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

The Pacific Decadal Oscillation (PDO) is a famous climate-ecology relationship. Mantua et al. (1997) and Hare et al. (1999) reported that Alaska salmon catch is high when the PDO is warm (positive), and that catch in Washington, Oregon and California (WOC) is low at the same time ("inverse production"). Beamish and Bouillon (1993) reported that the total North Pacific salmon catch follows the strength of the winter Aleutian Low. These papers used data to 1996 or earlier. Many people use these relationships to explain and forecast salmon production.

We tested the three claims with the North Pacific Anadromous Fish Commission (NPAFC) catch statistics (June 2026 release, commercial catch in numbers, 1925-2025). The forward period, 1997-2025, has 29 years that the authors did not use. It includes the strongest negative PDO values of the record (2020-2025). We wrote the plan (`files/code/ANALYSIS_PLAN.md`) before we calculated any post-1996 statistic. We tested 17 regional series: five species in Alaska, five in Southeast Alaska (SEAK), five in Canada, and coho and chinook in WOC.

Main results:

1. **Alaska: the PDO rule failed.** In 1925-1996, detrended Alaska catch correlated with the PDO during the marine residence of each species: pink r = +0.41, chum +0.43, sockeye +0.50, coho +0.35, chinook +0.26. In 1997-2025, the values were -0.07, -0.02, +0.43, +0.24 and +0.08. Only sockeye kept a clear positive association (90% interval +0.08 to +0.68). The PDO fell to record negative values after 2019, but Alaska catch stayed near its record high (Fig. 1A).
2. **WOC: the negative link held, and it was stronger than before.** For WOC coho, the detrended correlation changed from -0.29 (-0.53 to +0.01) to -0.55 (-0.77 to -0.23). The year-to-year correlation changed from -0.11 to -0.41 (-0.64 to -0.12). A model with the slope fitted in 1925-1996 forecast the 1997-2025 year-to-year change in WOC coho catch better than a random walk (skill +0.052, 90% block-bootstrap interval +0.019 to +0.088). WOC coho was the only one of 17 series that met our pre-set rule for "held". WOC chinook had a forward year-to-year correlation of -0.36 (-0.61 to -0.06), but its 1925-1996 slope had the wrong sign, so its fixed forecast had negative skill.
3. **The inverse production pattern stopped.** The detrended correlation between Alaska total catch and WOC coho+chinook catch changed from -0.47 (-0.71 to -0.13) to +0.13 (-0.19 to +0.43) (difference p = 0.03). Alaska and WOC chinook became positively correlated (levels +0.56, year-to-year +0.44): chinook catch decreased along the whole coast.
4. **The Aleutian Low rule did not repeat.** With the North Pacific Index (NPI) as a proxy for the Aleutian Low, total North Pacific pink, chum and sockeye catch had no clear negative correlation in 1950-1992 (r = -0.17, -0.45 to +0.13). In 1993-2025 it was positive (+0.39, +0.11 to +0.62), which is the opposite sign to the claim.
5. **Why the Alaska rule failed.** The PDO did not lose its link to regional sea temperature: the annual PDO-SST correlation for the Alaska boxes was +0.71 in 1925-1996 and +0.61 in 1997-2025 (difference p = 0.61); the WOC values were +0.69 and +0.53. Regional SST also lost its association with Alaska pink and chum catch. Thus the change is in the catch response, not in the index. In 1925-1996, the Alaska association came mostly from the contrasts between PDO regimes (1947 and 1977). Inside the 1977-1996 warm regime it was near zero for 4 of 5 species. The 1977 shift also came at the same time as a large increase of Alaska hatchery releases (pink and chum: 1 million fish in 1975, 1,528 million in 1996). When we added ln(hatchery releases) to a 1960-1996 regression, the PDO coefficient for Alaska pink catch decreased from 0.52 (SE 0.19) to 0.02 (SE 0.12), and for chum from 0.55 to 0.20. The published Alaska relationship therefore had few independent events and a strong confounder.
6. **Small year-to-year information remains.** If we let the 1925-1996 data select the PDO lag (0-4 years) for each series, the forward skill was larger than with 1,000 phase-randomized surrogate PDO series (mean skill +0.016 against a null mean of -0.030, p = 0.009; 11 of 17 series had positive skill against 6.4 expected, p = 0.04). The best single values were +0.16 (Alaska chinook) and +0.14 (Alaska chum). The pre-set marine-residence window had no skill above the null (p = 0.20). The mean gain is about 1.6% of the random-walk error. This is real but too small to be a useful forecast alone.

Conclusion for forecasting: the decadal "warm PDO, more Alaska salmon; fewer WOC salmon" rule is not robust enough to forecast catch. The southern-edge negative response of WOC coho to warm ocean conditions is the one part that held out of sample.

## 1. Question and prior work

Which published climate-ecology relationships stay true in new data? Earlier campaign work found failures or shrinkage for an Adelie penguin sea-ice curve, a night-light effect on leaf colour, a NestWatch heat contrast and a mountain pine beetle winter-cold effect (cited publications). Myers (1998) showed that many environment-recruitment correlations for fish failed when people tested them again. The PDO-salmon relationship is one of the most cited climate-ecology relationships, and it is used in management discussions. Litzow et al. (2018, 2020) showed that PDO-salmon covariance in the Gulf of Alaska decreased to near zero after 1988/89 (data to 2012 and 2019). Our work adds: (a) a forward test of the published claims on years after publication only, up to 2025, which includes the 2020-2025 negative PDO; (b) a coast-wide set of 17 regional series with WOC as the southern contrast; (c) forecast skill scores against a random walk, with a surrogate-index null for the whole family of tests; (d) a test of the inverse-production and Aleutian Low claims; (e) a decomposition of why the Alaska link failed (index coupling, regime contrasts, hatchery releases).

## 2. Data

- NPAFC Pacific salmonid catch statistics, updated June 2026 (1925-2025); commercial catch in thousands of fish. Entries "<0.5" and "<0.05" were set to half of the unit. Regions: Alaska whole state, Southeast Alaska, Canada whole country, WOC. Alaska sub-regions other than Southeast change their definitions in 1985, so we did not use them.
- NPAFC hatchery release statistics, June 2026 (Alaska, 1952-2025).
- NOAA NCEI ERSST v5 PDO index (monthly, to October 2026).
- NOAA ERSST v5 monthly SST (2 degree). Boxes: SEAK 54-60N 130-140W; central Gulf of Alaska 54-60N 140-160W; eastern Bering Sea 54-62N 158-172W (Alaska = mean of the three); BC 48-54N 124-134W; WOC 36-48N 122-128W. Anomalies are relative to the 1951-1980 monthly climatology.
- NCEP/NCAR Reanalysis 1 monthly sea-level pressure (1948-2026). NPI = area-weighted mean over 30-65N, 160E-140W, November-March. A low NPI means a strong Aleutian Low. Beamish and Bouillon used the Aleutian Low Pressure Index (ALPI). The NPI is a close proxy, but it is not the same index.

Exact files, hashes and terms are in `files/provenance/DATA_NOTICE.md` and `files/provenance/input_hashes.json`. The NPAFC files have no stated open licence, so the bundle does not contain them or annual catch tables made from them.

## 3. Methods

- Response: y = ln(catch). Covariate: the mean monthly index from January of the ocean-entry year (t - L) to March of the catch year t. L = 1 for pink and coho, 2 for sockeye, 3 for chum and chinook. Expected sign: positive for Alaska and SEAK, negative for WOC, none for Canada.
- Periods: 1925-1996 (published era) and 1997-2025 (forward). For the Aleutian Low claim: 1950-1992 and 1993-2025.
- Correlations: levels (as in the papers), linearly detrended levels within each period (added after the plan, because joint trends dominate the levels), and year-to-year differences (2-year differences for pink, to keep odd and even lines apart). Intervals use the effective sample size of Pyper and Peterman (1998); differences between periods use Fisher z.
- Forecasts: the difference model dy = b dX, with b fitted in 1925-1996 and applied to observed 1997-2025 dX. Baseline: random walk (dy = 0). Skill = 1 - MSE(model) / MSE(random walk). Intervals from a moving-block bootstrap of years (block 5, 2,000 draws). A rolling-origin version refits b each year with all earlier years.
- Family-wise null: 1,000 phase-randomized surrogate monthly PDO series (same spectrum, no link to catch) go through the same pipeline. We compare the mean skill and the number of series with positive skill.
- Pre-set decision rule: a claim "held" if the forward correlation had the published sign with a 90% interval that excluded zero, and the fixed forward skill was positive with a bootstrap interval that excluded zero.
- Explanations (after the tests): PDO-regional SST correlations by period; sub-period correlations; Alaska regressions of ln catch on PDO with and without ln(hatchery releases in the ocean-entry year), 1960-1996 and 1997-2025, with HAC (Newey-West, 3 lags) errors.

## 4. Results

### 4.1 Alaska, SEAK and Canada

Figure 2 shows all 17 PDO correlations. Before 1997, Alaska detrended correlations were positive for all five species (four of five intervals above zero). After 1996, only sockeye stayed clearly positive (+0.43, +0.08 to +0.68). SEAK correlations were +0.07 to +0.40 before and -0.27 to +0.09 after. Year-to-year correlations were near zero for Alaska in both periods (-0.02 to +0.09 before, -0.14 to +0.17 after), so the original Alaska link was a low-frequency link. In Canada, catch decreased strongly after the 1990s because of fishery closures, and no correlation had a clear and stable sign. SEAK chinook (many of these fish come from rivers in BC and WOC, and the Pacific Salmon Treaty sets the catch limit) had a negative forward year-to-year correlation (-0.30), like WOC.

Regional SST gave the same pattern as the PDO for Alaska pink and chum (detrended forward r = -0.03 and -0.08). For Alaska sockeye, both SST and PDO stayed positive (+0.39 and +0.43).

### 4.2 WOC

WOC coho and chinook kept negative correlations with the PDO and with WOC SST in 1997-2025 (Fig. 2). For WOC coho, the result did not depend on the 2014-2017 marine heatwave: without these years, the forward year-to-year r was -0.34; the leave-one-year-out range was -0.48 to -0.15. For WOC chinook the values were -0.27 and -0.45 to -0.25. The level of WOC catch decreased strongly after the early 1990s because of fishery closures and Endangered Species Act listings (Fig. 1B). This decrease is not a PDO effect, and our detrended and difference tests remove most of it.

### 4.3 Inverse production and the Aleutian Low

See `files/results/c2_inverse.csv` and `c3_aleutian.csv`. The Alaska-WOC negative correlation stopped after 1996 (levels -0.49 to +0.09, p = 0.04; detrended -0.47 to +0.13, p = 0.03). Total North Pacific pink, chum and sockeye catch increased from at most 477 million fish per year before 2000 to a record 720 million in 2023, mostly because Russian catch increased (27 million in 1960, 475 million in 2018). The NPI correlation was positive after 1992.

### 4.4 Forecast skill

Figure 3A shows the forward skill per series. The pre-set marine-residence model had skill above zero with an interval above zero only for WOC coho (+0.052). Its mean skill over 17 series (+0.001) was not above the surrogate null (p = 0.20). The training-selected lag model had higher forward skill than the null (Fig. 3B; p = 0.009). This shows that the PDO contains some year-to-year information at specific lags, but the gain is small (mean 1.6% of the random-walk error, maximum 16%).

### 4.5 Why the Alaska link failed

- Not because the PDO stopped tracking regional SST (`pdo_sst_coupling.csv`: all period differences had p >= 0.20).
- The 1925-1996 association depends on few regime contrasts. In the 1977-1996 warm regime alone, level correlations were -0.20 (pink), +0.47 (chum), +0.03 (sockeye), -0.01 (coho) and -0.09 (chinook) (`subperiod_levels.csv`).
- Hatchery releases increased at the same time as the 1977 shift. With releases in the model, the 1960-1996 PDO coefficient decreased by 96% for pink, 63% for chum, 55% for sockeye, 37% for coho and 36% for chinook (`ak_hatchery_models.csv`). Releases are almost a step function of time in this period, so this test cannot separate hatcheries from other changes of the late 1970s, such as the 200-mile fishery zone (1976) and limited entry (1973). In 1997-2025 the PDO coefficient was near zero for pink, chum and sockeye with or without releases.

## 5. Limitations

- Catch is not abundance. Management, effort, markets and fishery closures change catch. The original claims used catch, so our test is fair to them, but catch is a weak measure of production. A test with run-size or recruits-per-spawner data would be stronger.
- The statewide Alaska series mixes many stocks with different responses (for example, record Bristol Bay sockeye and very low Yukon chinook and chum in 2021-2022).
- The lags and windows are simple. Other plausible windows exist; the training-selected lag test shows that the choice changes the year-to-year result.
- The NPI is a proxy for the ALPI and starts in 1948, so our test of Beamish and Bouillon covers a shorter training period than theirs.
- The forward period is 29 years, with about 2-3 PDO phase changes. Intervals for level correlations are wide (effective n 11-29).
- The detrended level test and all explanation analyses were added after the plan. The surrogate test used the pre-set series and windows.
- WOC catch after 1995 is small and strongly managed; part of its year-to-year variation can come from regulations that respond to ocean forecasts.

## 6. Reproduction

1. `bash files/code/fetch_data.sh SCRATCH` downloads the five input files into a scratch folder and checks the SHA-256 hashes (use a folder outside this bundle).
2. `cd files/code; DATA_ROOT=SCRATCH DERIVED=SCRATCH/derived bash run_all.sh`. The scripts write result tables and figures to `files/out/`. With the inputs listed above, they gave the bundled tables byte for byte (tested on the campaign machine; about 3 minutes). Python 3.12 with numpy, pandas, xarray, netCDF4, scipy, statsmodels, matplotlib and openpyxl.

Files: `files/code/` (plan, scripts), `files/results/` (aggregate statistics only), `files/figures/`, `files/provenance/`.

## 7. References

- Mantua NJ, Hare SR, Zhang Y, Wallace JM, Francis RC (1997) A Pacific interdecadal climate oscillation with impacts on salmon production. Bull. Am. Meteorol. Soc. 78:1069-1079.
- Hare SR, Mantua NJ, Francis RC (1999) Inverse production regimes: Alaska and West Coast Pacific salmon. Fisheries 24(1):6-14.
- Beamish RJ, Bouillon DR (1993) Pacific salmon production trends in relation to climate. Can. J. Fish. Aquat. Sci. 50:1002-1016.
- Litzow MA, Ciannelli L, Puerta P, Wettstein JJ, Rykaczewski RR, Opiekun M (2018) Non-stationary climate-salmon relationships in the Gulf of Alaska. Proc. R. Soc. B 285:20181475.
- Litzow MA, Hunsicker ME, Bond NA, et al. (2020) The changing physical and ecological meanings of North Pacific Ocean climate indices. PNAS 117:7665-7671.
- Pyper BJ, Peterman RM (1998) Comparison of methods to account for autocorrelation in correlation analyses of fish data. Can. J. Fish. Aquat. Sci. 55:2127-2140.
- Myers RA (1998) When do environment-recruitment correlations work? Rev. Fish Biol. Fish. 8:285-305.
- Mueter FJ, Peterman RM, Pyper BJ (2002) Opposite effects of ocean temperature on survival rates of 120 stocks of Pacific salmon in northern and southern areas. Can. J. Fish. Aquat. Sci. 59:456-463.
- Data: NPAFC (2026) catch and hatchery release statistics; Huang et al. (2017) ERSST v5; Kalnay et al. (1996) NCEP/NCAR Reanalysis.
