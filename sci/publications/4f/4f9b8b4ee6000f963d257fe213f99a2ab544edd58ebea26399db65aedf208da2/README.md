# Stock-specific warming effects on fish surplus production changed with assessment revisions and did not improve forecasts of later years in RAM Legacy v4.66

**Job:** sci-1107-hp-climate-pollution-biodiversity-b0e0b94a237b · **Campaign:** 11_07_2026 · **Topic:** climate-pollution-biodiversity · **Machine:** hp · **Account:** claude-olen · **Model:** claude-opus-5-5 (Anthropic). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Free et al. (2019, *Science* 363:979) fitted a surplus-production model with a sea-surface-temperature (SST) term to 235 fish and invertebrate stocks in the RAM Legacy Stock Assessment Database v3.8:

P_t = (r/p) · B_t · (1 − (B_t/K)^p) · exp(θ · SST_t) + AR(1) error, with p = 0.55.

Each stock has its own temperature effect θ. The paper reports stocks with significantly negative and positive θ and uses θ to hindcast a 4.1% decrease in maximum sustainable yield from 1930 to 2010. These stock-specific θ values are the type of climate response that managers want to use for forecasts. Earlier campaign work found that published climate-ecology relationships often fail or shrink in newer data (Adélie penguins, leaf colour, NestWatch, mountain pine beetle, North Sea fishes). Nobody has tested the Free et al. θ values with the newer assessments.

We asked four questions:

1. **Reproduction.** Can a per-stock fixed-effect version of the model reproduce the published θ from the published input table?
2. **Revision.** Do the θ values stay the same when the same stocks and years are refitted with the revised assessments in RAM Legacy v4.66 (2024)?
3. **Forward stability.** Is θ in the years after each stock's original end year (median forward period 2010-2017; range 2001-2022) the same as θ before? We compare the observed agreement with the agreement that we expect if θ is constant.
4. **Forecast skill.** Does the SST term decrease the error of one-step-ahead forecasts of surplus production in those later years?

We wrote the plan (`files/PLAN.md`) before we opened the v4.66 time series. The plan file also lists seven deviations.

## 2. Data and methods

- **Original analysis.** Free et al. repository (GitHub `cfree14/sst_productivity`, commit `cd1d12ab`): the input table with scaled total biomass (TB), surplus production (SP) and stock SST series, and the output table with published θ (fixed-effect and random-effect fits, COBE SST).
- **New assessments.** RAM Legacy v4.66 (Zenodo 14043031, CC BY 4.0). We matched stocks by stock id (202 of 235), plus two pure id changes from the v4.66 change history. We used the assessment TB and the catch type that Free et al. used (TC or TL, else TCbest). We excluded 5 stocks because TB or catch was not in metric tonnes. SP_t = TB_{t+1} − TB_t + C_t. We scaled TB and SP by the maximum TB in the original years.
- **Stock SST.** The stock boundary shapefiles are not public. Thus we emulated each stock's SST series as the area-weighted annual mean of ERSST v5 cells within a circle around the published stock centroid. The circle radius is m·√(area/π), and m ∈ {0.5, 0.75, 1, 1.5, 2} gives the smallest RMSE against the Free et al. ERSST series. This step used only SST data. The median correlation with the Free et al. series was 0.990 (detrended 0.988; RMSE 0.15 °C), and 229 of 235 stocks had r ≥ 0.8. HadISST1 gave the same match quality and was a sensitivity test.
- **Model fit.** We used maximum likelihood per stock with the same likelihood as the fixed-effect TMB model of Free et al. (AR(1) process error, B0 ≤ 5 penalty). We profiled out r and σ in closed form. "Well-identified" stocks have a finite θ SE and no parameter at a bound.
- **Periods.** "Pre" = the years that Free et al. used for each stock (end year median 2009). "Forward" = later years with SP in v4.66. 91 well-identified stocks had ≥ 5 forward years (742 stock-years). 54 stocks had ≥ 8 forward years.
- **Forward θ.** θ in forward years with B0, r and ρ fixed at the pre-period fit. We also used a joint model with separate pre and forward θ (likelihood-ratio test).
- **Forecasts.** We fitted all models on pre years of v4.66 only. Then we made one-step forecasts of forward SP with observed B_t, SST_t and the previous residual. Model (a) has θ = 0. Model (b) has θ refitted on v4.66. Model (c) has θ fixed at the published random-effects value. Exploratory variants: (d) empirical-Bayes shrunk θ, (e) one common θ, and (rw) last-year SP. Skill = 1 − SSE/SSE(a). We give the per-stock median, the share of stocks with skill > 0, and pooled skill with σ-standardised errors. The 95% intervals come from 2,000 stock bootstraps.
- **Constant-θ reference.** For each forecast stock, we simulated SP from its fitted pre-period model (b) with observed biomass and SST and Gaussian AR(1) errors (100 replicates). Then we refitted (a) and (b) on the simulated pre years and scored the forward years as for the real data. This shows how much agreement and skill to expect if θ does not change. The comparison includes estimation noise and short forward series.

## 3. Results

### 3.1 Reproduction (Q1)
With the published input table and COBE SST, our θ agreed with the published fixed-effect θ for 225 well-identified stocks: Spearman 0.92, sign agreement 96%, median absolute difference 0.018. Of the 40 stocks with significant published fixed-effect θ, 38 were also significant in our fit (Figure 1A). For 8 stocks, the profile fit went to a parameter bound or had no finite SE, and 3 published fits had no SE. The published fit uses a Laplace step over θ, which can give finite values where a profile fit does not.

### 3.2 Assessment revision (Q2)
- The SST emulation alone (v3.8 data, emulated ERSST compared with published COBE fit) gave Spearman 0.83 and median |Δθ| 0.12.
- The assessment revision alone (same years, same emulated SST, v3.8 compared with v4.66 data) gave Spearman 0.73, Pearson 0.37, sign agreement 83% and median |Δθ| 0.057 (191 stocks; Figure 1B). With HadISST it gave Spearman 0.61.
- For 40% of stocks, the v4.66 surplus-production series for the same years had a correlation below 0.9 with the v3.8 series. For 15% of stocks, the correlation was below 0.5. The θ change increased with the SP revision (Spearman −0.75 between SP correlation and |Δθ|). Stocks with unchanged series kept their θ.
- The published random-effects table marks 14 stocks as significant (9 negative, 5 positive). 11 of them are well-identified in v4.66. 10 of the 11 kept their sign, and 6 kept a significant θ of the same sign (HadISST: 9 and 5).

### 3.3 Forward stability (Q3), 91 stocks with ≥ 5 forward years

| Statistic | Observed | Expected if θ is constant (mean, 95% range) | One-sided p |
|---|---|---|---|
| Spearman, θ pre vs θ forward | 0.18 | 0.41 (0.22 to 0.59) | 0.02 |
| Median absolute θ change | 0.62 | 0.37 (0.29 to 0.50) | < 0.01 |
| Sign agreement | 60% | 66% (57% to 75%) | 0.13 |

The joint model gave a summed likelihood-ratio statistic of 181 on 91 df (χ² p = 6 × 10⁻⁸). The per-stock test was positive at p < 0.05 for 16% of stocks. The χ² reference can be anti-conservative for short series, but the simulation comparison above does not use it. With HadISST the Spearman correlation was 0.33. With ≥ 8 forward years (54 stocks) it was 0.02 (Figure 1C, Figure 3A).

### 3.4 Forecast skill (Q4), 91 stocks, 742 forward stock-years

| Forecast model | Median per-stock skill (95% CI) | Stocks better than θ = 0 | Pooled skill (95% CI) |
|---|---|---|---|
| (b) θ refitted on v4.66 pre years | −0.026 (−0.118 to 0.007) | 45% | −2.5 (−9.2 to −0.11) |
| (c) θ published (random effects) | +0.0007 (−0.006 to 0.011) | 54% | +0.11 (−0.02 to 0.23) |
| (d) shrunk θ (exploratory) | +0.0001 (−0.013 to 0.007) | 51% | −0.11 (−0.41 to 0.06) |
| (e) common θ (exploratory) | 0.0000 | 51% | −0.002 (−0.009 to 0.004) |
| (rw) last-year SP (exploratory) | −0.083 (−0.233 to 0.040) | 43% | +0.18 (−0.09 to 0.42) |
| Expected for (b) if θ is constant | +0.008 (−0.012 to 0.036) | 53% (45% to 62%) | heavy-tailed, not used |

- The refitted θ made the typical forecast worse. Its median skill was lower than all 100 constant-θ simulations (p < 0.01). The share of stocks with a better forecast (45%) was at the lower 5% of the simulated range (p = 0.05).
- The published, strongly shrunk θ was neutral for the typical stock. Its positive pooled skill came from a few stocks with fitted ρ ≥ 0.99. Without these 10 stocks, its pooled skill was −0.015 (−0.06 to 0.03). With HadISST, the pooled skill was +0.10 (0.0003 to 0.21), and the median skill was again about zero.
- **Even if θ were constant, the expected gain is small.** The median per-stock improvement was only +0.8%, and only about 53% of stocks were expected to improve. Year-to-year process error in surplus production is much larger than the SST signal at the scale of one stock (Figure 2A, Figure 3B).
- Forward errors of the θ = 0 model had a median ratio of 0.84 to the pre-period process variance. The constant-θ simulation expected 1.21 (1.02 to 1.38). A few stocks had very large forward errors (pooled ratio 2.75). Thus terminal assessment years are smoother than the earlier years for most stocks, and a few stocks have structural breaks (Figure 2B).

## 4. Interpretation

The stock-specific warming effects of Free et al. are reproducible from their own table. But they are not stable properties of the stocks in the form that a forecast needs:

1. A large part of the θ variation comes from the assessment version. A new assessment of the same years changes the surplus-production series, and θ changes with it. A θ value is thus a property of the stock and of the assessment model.
2. In later years, θ agreed with the earlier θ less than estimation noise alone predicts (Spearman 0.18 compared with an expected 0.41).
3. The refitted stock-specific θ made one-step forecasts of surplus production worse. The published random-effects θ, which is shrunk strongly toward zero, was approximately neutral. A forecast with θ = 0 was as good as any SST-based forecast that we tested.

This result does not show that warming has no effect on fish productivity. The fleet-level MSY change of Free et al. is an average over many stocks and long periods. Our test covers stock-level, year-to-year forecasts over about 8 years per stock. But it shows a clear limit: stock-specific temperature–production slopes from assessment outputs are not robust enough to forecast surplus production for individual stocks at present. This agrees with other campaign results. For example, sea-temperature slopes did not forecast later North Sea fish length-at-age or distribution.

## 5. Limitations

- Stock SST is emulated from published centroids and areas, not from the original polygons. It matched the original series closely (median r 0.99), but it is not identical, and the emulation alone changed θ (Spearman 0.83 with published θ).
- We used per-stock fixed-effect maximum likelihood, not the hierarchical random-effects TMB model. We used the published random-effects θ only as a fixed forecast input (model c).
- Forward periods are short (median 8 years; 91 stocks with ≥ 5 years). The tests have low power for single stocks. Thus our result is about the set of stocks, not about each stock.
- The v4.66 "forward" years are assessment outputs. Terminal years of an assessment are less certain and often smoother. This explains forward errors below the in-sample level. The forward-year data are thus not independent observations.
- The AR(1) ρ is unconstrained, as in Free et al. Ten forecast stocks had ρ ≥ 0.99. For them, the simulation used ρ clipped at 0.99 (deviation 7). We report sensitivity results without these stocks.
- 31 of the original stocks are absent, split, merged or redefined in v4.66, 5 have non-tonne units, and 2 have fewer than 15 pre-period years in v4.66. The tested set is not a random sample of the 235 stocks.
- The constant-θ simulation holds the observed biomass fixed and treats the pre-period estimates as true values. Pooled simulated skill is heavy-tailed, and we did not use it.

## 6. Files and reproduction

- `files/PLAN.md` — the plan, with time stamps and the seven deviations.
- `files/DATA_SOURCES_AND_NOTICES.md` — external data versions, URLs, SHA-256 hashes, terms and what the bundled tables contain. External data are not bundled.
- `files/code/` — `fetch_data.sh` (gets external data into local scratch), `spmodel.py` (model), `s01_emulate_sst.py`, `s02_reproduce_free.py`, `s03_forward_test.py`, `s03b_shrinkage_variants.py`, `s03c_series_revision.py`, `s04_stationary_sim.py`, `s05_analyse_and_plot.py`, `s06_export_public_tables.py`.
- `files/results/summary.json` — all aggregate statistics in this README. Per-stock tables contain only our estimates (see the notice file). `q34_stationary_sim_summary_by_rep.csv` has the simulated statistics for each replicate.
- `files/figures/` — Figures 1-3.

To reproduce, run from the worktree root with Python 3.12, numpy, scipy, pandas, xarray, netCDF4, matplotlib, pyarrow and python-calamine. Set OMP_NUM_THREADS=1.

```
bash work/result/files/code/fetch_data.sh .
python work/result/files/code/s01_emulate_sst.py ersst
python work/result/files/code/s01_emulate_sst.py hadisst
python work/result/files/code/s02_reproduce_free.py
python work/result/files/code/s03_forward_test.py ersst TB
python work/result/files/code/s03_forward_test.py hadisst TB
python work/result/files/code/s03_forward_test.py ersst TBbest
python work/result/files/code/s03b_shrinkage_variants.py ersst TB
python work/result/files/code/s03c_series_revision.py
python work/result/files/code/s04_stationary_sim.py ersst TB 100 5
python work/result/files/code/s04_stationary_sim.py ersst TB 100 5 clip
python work/result/files/code/s05_analyse_and_plot.py
python work/result/files/code/s06_export_public_tables.py
```

s05 needs the full tables from s02-s04 (s06 removes the third-party columns after s05). On the hp host (load 50-80 on 8 cores), s03 took about 20 min and s04 about 60 min with 6 processes.

## 7. References

- Free CM, Thorson JT, Pinsky ML, Oken KL, Wiedenmann J, Jensen OP (2019) Impacts of historical warming on marine fisheries production. *Science* 363:979-983. doi:10.1126/science.aau1758
- Szuwalski C (2019) Comment on "Impacts of historical warming on marine fisheries production", https://repository.library.noaa.gov/view/noaa/55980 ; Free et al. (2019) Response to Comment, https://repository.library.noaa.gov/view/noaa/53173
- RAM Legacy Stock Assessment Database v4.66 (2024), doi:10.5281/zenodo.14043031; Ricard D et al. (2012) *Fish and Fisheries* 13:380-398, doi:10.1111/j.1467-2979.2011.00435.x
- Huang B et al. (2017) ERSST v5. *J. Climate* 30:8179-8205, doi:10.1175/JCLI-D-16-0836.1
- Rayner NA et al. (2003) HadISST1. *J. Geophys. Res.* 108:4407, doi:10.1029/2002JD002670
