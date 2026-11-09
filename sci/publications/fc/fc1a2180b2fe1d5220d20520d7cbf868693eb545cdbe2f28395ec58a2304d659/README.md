# Carabid trends at 12 UK ECN sites in 1994-2008 did not predict trends in 2009-2015, and species thermal affinity did not explain the declines

## Summary

We used the UK Environmental Change Network (ECN) ground beetle (Carabidae) pitfall data for 1992-2015 at 12 sites. Brooks et al. (2012) reported large declines in this network for 1994-2008. We did an out-of-sample test with the 2009-2015 data, which that study did not use. We also tested one climate explanation: if warming causes the declines, species from cool climates must decrease more than species from warm climates.

We controlled for three sources of observation bias: trap effort (valid trap-days), changes in the season coverage and transects, and the activity response of pitfall catches to the temperature during each two-week trap period.

Main results:

1. **The 1994-2008 decline repeats in our analysis.** For 211 species-site series (69 taxa, 12 sites), the median trend was -4.4% per year (bootstrap 95% CI -7.2% to -2.3%). 64% of the series had a negative slope.
2. **The trends of individual series did not continue.** In 2009-2015, the median trend was +1.7% per year (95% CI -3.8% to +9.3%; 118 series, 10 sites). The 1994-2008 and 2009-2015 slopes of the same 111 series had no correlation (Spearman rho = -0.09, p = 0.34). Of 71 series with a negative 1994-2008 slope, 33 (46%) had a negative 2009-2015 slope.
3. **Trend extrapolation was a worse forecast than the recent level.** For the 2009-2015 catch total of 157 series, the extrapolated 1994-2008 trend had a mean squared log error of 3.00. The mean 2004-2008 level had an error of 1.83 (skill of the trend = -0.64, taxon-bootstrap 95% CI -1.02 to -0.36). The same failure occurred inside the 1994-2008 period (fit 1994-2001, forecast 2002-2008: skill -1.08) and with each site left out.
4. **The average abundance stayed low.** The median 2009-2015 catch was 17% below the 2004-2008 level (log ratio -0.18, 95% CI -0.51 to -0.05). Thus there was no general recovery. On average the extrapolated trend had no bias (median log ratio -0.06, CI -0.48 to +0.34), but its errors for single series were large.
5. **At the site level, the declines stopped.** For all carabids together, the 1994-2008 trend was clearly negative (-8% to -21% per year) at 7 of 10 sites with 2009-2015 data. At all 7 sites, the 2009-2015 catch was equal to or above the extrapolated decline (log ratio +0.01 to +1.54). At the 2 sites with increases (Alice Holt, Porton Down), the 2009-2015 catch was below the extrapolated increase (log ratio -1.30 and -1.22).
6. **Species thermal affinity did not predict the trends.** We calculated a species temperature index (STI) from GBIF occupancy in Europe and the 1961-1990 GHCN-CAMS temperature. The slope of the trend on STI was +0.010 per C (SE 0.008, p = 0.19) in 1994-2008 and +0.017 per C (SE 0.018, p = 0.34) in 2009-2015. Results in the cool north/west sites and the warm south sites were the same (all p > 0.09). The community temperature index (CTI) had no trend (-0.009 C per decade, SE 0.012).
7. **The catch had a temperature activity bias, but this bias did not change the conclusions.** A trap period that was 1 C warmer than normal caught 9.1% more beetles (inverse-variance weighted mean of 224 species-site series; 76% of the coefficients were positive). Adjustment for this bias changed the median slope by -0.9% per year in 1994-2008 and by +1.7% per year in 2009-2015. The median absolute change of a single slope was 0.6% per year (1994-2008) and 1.2% per year (2009-2015). The annual CTI increased by 0.034 C for each 1 C of May-October warmth (p = 0.01) after the adjustment. This effect is small.

Conclusion: the ECN carabid declines of 1994-2008 are real in these data. But the trends of single species at single sites were not persistent, and they were not a reliable forecast for 2009-2015. The declines were not ordered by species thermal affinity. Thus the data do not support climate warming as the main cause of the declines. Other causes (for example habitat and management changes, or density changes that are not persistent) stay possible. We did not test them.

## Question and prior work

- Brooks D.R. et al. 2012. Large carabid beetle declines in a United Kingdom monitoring network increases evidence for a widespread loss in insect biodiversity. Journal of Applied Ecology 49:1009-1019. doi:10.1111/j.1365-2664.2012.02194.x. This study used ECN data for 1994-2008. It reported that three quarters of the species decreased, with the largest decreases at northern and upland sites.
- Earlier campaign publications used the same ECN carabid data for catch timing and trap flooding (see citations). They did not test long-term abundance trends. One campaign publication on ECN moths found a warm-night catch effect of 14% per 1 C. Our 9% per 1 C activity effect for carabids agrees with that type of bias.

Our questions:

1. Did the 1994-2008 trends continue in 2009-2015, at the level of single species-site series and of the full network?
2. Did species with a low STI (cool-climate species) decrease more than species with a high STI, in two independent periods and in two groups of sites?
3. How much does the activity response of pitfall catches to temperature change these results?

## Data

All shared inputs were read in place from the campaign dataset store. We did not change them.

| Input | Shared path | Source | SHA-256 |
| --- | --- | --- | --- |
| ECN carabid counts 1992-2015 (ECN_IG1.csv) | `datasets/ecn-carabid-ig1-1992-2015-eidc-8385f864/ECN_IG1.csv` | EIDC, doi:10.5285/8385f864-dd41-410f-b248-028f923cb281 | `861de852872da466dfa44e1e75a6977821c3d84b77963da740c007d8893291dd` |
| ECN supporting documents (trap dates IG2, species codes, quality text) | `datasets/ecn-carabid-supporting-docs-eidc-8385f864/ECN_IG_supporting_documents.zip` | https://data-package.ceh.ac.uk/sd/8385f864-dd41-410f-b248-028f923cb281.zip | `0935a9fdb8a055b2a37972ebf25c00721d523fcfdfe7aac537f9ccb1358d6b76` |
| E-OBS v31.0e daily mean temperature, 0.25 deg ensemble mean | `datasets/eobs-v31.0e-tg-ens-mean-0.25deg/tg_ens_mean_0.25deg_reg_v31.0e.nc` | KNMI ECA&D (Cornes et al. 2018, doi:10.1029/2017JD028200) | `7d35a58a02767361a5dfdbe92052a9482d585474e0aaa8e0a0cb0b117bd25684` |
| GHCN-CAMS monthly land air temperature, 0.5 deg | `datasets/psl-ghcncams-air-mon-mean-20261105/air.mon.mean.nc` | NOAA PSL (Fan and van den Dool 2008, doi:10.1029/2007JD008470) | `8dbe8e8ce86729f56a2234dec7420b94aecba804aa7df599c8fea68ade70802b` |
| GBIF occurrence density tiles (records 1970-2025) | not shared; archived here as `files/raw/gbif_density_tiles_20261109.tar.gz` | GBIF maps API v2, retrieved 2026-11-09 | see archive |

GBIF recipe: for each taxon, `https://api.gbif.org/v1/species/match?name=<name>&family=Carabidae&kingdom=Animalia`, then `https://api.gbif.org/v2/map/occurrence/density/2/{x}/{y}.mvt?srs=EPSG:4326&taxonKey=<acceptedKey>&bin=square&squareSize=32&year=1970,2025` for x = 3, 4, 5 and y = 0, 1. GBIF data are from many datasets with CC0 or CC BY licences. The density tiles do not have a download DOI. Thus we archived the raw tiles.

## Methods

**Trap samples.** Each ECN site has three or more transects of 10 pitfall traps. Traps are emptied every two weeks from May to October. We removed trap samples with a quality code for lost, flooded, damaged, opened, partly lost or debris-filled traps (codes 100-103, 135, 160-162, 164, 165, 167). We summed the valid traps for each transect and date. Effort is the sum of valid trap-days. The trap start dates come from ECN_IG2. If a start date was missing or not plausible, we used 14 days. We kept trap periods with a mid-date in May-October and assigned each to one of 13 season periods of 14 days. Records at genus level were removed. We merged *Pterostichus nigrita* and *P. rhaeticus* (and "nigrita sens. str."), and *Trechus obtusus* and *T. quadristriatus*, because these pairs are often confused. Result: 8,808 transect samples, 46 transects, 76 taxa with 50 or more individuals.

**Trap-period temperature.** For each trap period we calculated the mean E-OBS daily temperature at the nearest 0.25 deg cell to the site. The anomaly (`tanom`) is this mean minus the mean for the same site and season period.

**Annual index.** For each taxon and site (30 or more individuals and 5 or more years with catches), we fitted a Poisson GLM at the sample level: `count ~ transect + season period + year (factor) [+ beta * tanom] + offset(log trap-days)`. Because year is a factor, beta comes only from differences between trap periods in the same year. Thus beta measures the short-term activity response of the catch, not a population change. The expected count E of each sample uses the transect, season-period and effort terms. For the adjusted version, E also includes beta * tanom. The annual index is O/E, where O is the observed catch in the year.

**Trends.** For each series and window we fitted a year-level quasi-Poisson model: `O_y ~ offset(log E_y) + a + b * year`. The dispersion is the Pearson chi-square divided by (n - 2). Thus the variation between years sets the uncertainty. Windows: P1 = 1994-2008 (8 or more years, 5 or more years with catches, 20 or more individuals), P2 = 2009-2015 (4 or more years, 3 or more years with catches, 10 or more individuals). We summarised the slopes with the median (bootstrap CI over series) and a DerSimonian-Laird random-effects mean.

**Forecast test.** We fitted the P1 models and forecast the 2009-2015 total catch with the known 2009-2015 effort, transects and season coverage. We compared three forecasts: (1) the P1 log-linear trend, (2) the P1 mean level, (3) the 2004-2008 mean level. The error is log((O + 0.5) / (forecast + 0.5)). Skill = 1 - MSLE(trend) / MSLE(2004-2008 level). We used a bootstrap over taxa for the confidence intervals. As a placebo, we did the same test inside P1 (fit 1994-2001, forecast 2002-2008, recent level 1997-2001). We also removed each site in turn, and we removed Hillsborough 2001-2003. In those years, ECN cannot separate empty traps from traps that did not operate.

**Species temperature index (STI).** For each taxon we took the GBIF occupied squares (0.35 deg, records 1970-2025) in the box 25 W-60 E, 34-72 N. We assigned them to 0.5 deg GHCN-CAMS cells. STI is the mean 1961-1990 annual temperature over the occupied cells, with equal weight for each cell. A May-October STI was used as an alternative. Example values: *Pterostichus adstrictus* 2.7 C, *Calathus micropterus* 4.1 C, *P. madidus* 9.2 C, *Syntomus (Metabletus) obscuroguttatus* 10.3 C. Old ECN names were matched to accepted GBIF names. *Calathus piceus* was matched to *C. rotundicollis*.

**STI tests.** We regressed the slopes on STI with site fixed effects. Weights are 1/(SE^2 + tau^2). Standard errors are clustered by taxon. We did the test for P1, P2 and 1994-2015, for all sites, and for two groups of sites. The cool north/west group has a 1961-1990 May-October mean below 12.5 C (Glensaugh, Hillsborough, Moor House, Sourhope, Snowdon, Cairngorms). The warm south group has the other six sites.

**CTI.** For each site and year, CTI = sum(w * STI) / sum(w), with w = log(1 + A) and A = index times the mean annual catch of the taxon at the site. The taxa set is fixed for each site. We regressed the CTI anomaly on the May-October temperature anomaly and on year (site-centred values, SE clustered by year).

## Results tables

Network trends (adjusted index; `files/results/network_trends.csv`):

| Window | Series | Taxa | Sites | Median slope (%/yr) | 95% CI (%/yr) | Share negative |
| --- | --- | --- | --- | --- | --- | --- |
| 1994-2008 | 211 | 69 | 12 | -4.4 | -7.2 to -2.3 | 0.64 |
| 2009-2015 | 118 | 52 | 10 | +1.7 | -3.8 to +9.3 | 0.47 |
| 1994-2015 | 209 | 69 | 12 | -4.3 | -5.7 to -2.7 | 0.67 |

Forecast of 2009-2015 totals (adjusted; `files/results/forecast_summary.csv`, `forecast_robustness.csv`):

| Test | Series | MSLE trend | MSLE recent level | Skill (95% CI) |
| --- | --- | --- | --- | --- |
| Fit 1994-2008, forecast 2009-2015 | 157 | 3.00 | 1.83 | -0.64 (-1.02 to -0.36) |
| Placebo: fit 1994-2001, forecast 2002-2008 | 149 | 3.36 | 1.61 | -1.08 (-1.98 to -0.48) |
| Main test without Hillsborough 2001-2003 | 156 | 3.01 | 1.84 | -0.63 (-0.98 to -0.35) |
| Leave one site out (10 runs) | 127-153 | 2.82-3.19 | 1.69-1.98 | -0.80 to -0.58 |

STI slope tests (adjusted; slope of trend per 1 C of STI; `files/results/sti_tests.csv`):

| Window | All sites | Cool north/west | Warm south |
| --- | --- | --- | --- |
| 1994-2008 | +0.010 (SE 0.008) | +0.009 (0.012) | +0.011 (0.011) |
| 2009-2015 | +0.017 (0.018) | +0.009 (0.027) | +0.033 (0.022) |
| 1994-2015 | +0.003 (0.007) | +0.005 (0.012) | +0.000 (0.008) |

The raw (not temperature-adjusted) results are in the same files (`ver = raw`). They are very similar.

## Figures

- `files/figures/fig1_site_totals.png`: all carabids per site, 1994-2008 trend, its extrapolation, and the 2009-2015 observations.
- `files/figures/fig2_forecast.png`: forecast errors of three forecasts, P1 against P2 slopes, and trend skill with placebo and leave-one-site-out results.
- `files/figures/fig3_sti_cti_activity.png`: slopes against STI in the two periods, CTI against season temperature, and the activity bias.

## Limitations

- The out-of-sample period is short (4-7 years) and has data at only 10 sites. Two sites stop in 2009 and 2011. Single-series slopes for 2009-2015 are very uncertain. A paired test of P2 against P1 slopes was not significant (Wilcoxon p = 0.59). Thus we do not claim that the network trend changed sign. We claim that series-level trends did not persist and were not a good forecast.
- The 1994-2008 trend extrapolation also failed inside 1994-2008. Thus the failure is a general property of these 7-15 year series. It is not specific evidence of a change after 2008.
- Pitfall catches measure activity-density, not population size. Our temperature adjustment uses only the short-term activity response in the same year. Other effects on catchability (vegetation height, rain, flooding, trap changes, identification changes) are not removed.
- The STI comes from GBIF occurrence data with strong differences in recording effort between countries. We used equal weight for each occupied cell to decrease this effect. The STI does not include ranges outside the European box.
- With 12 sites, site-level tests (for example of nitrogen deposition or land management) have low power. We did not test them.
- E-OBS cells (0.25 deg) do not show the local altitude of upland sites. We used only anomalies.
- Brooks et al. (2012) used a different statistical method. Our 1994-2008 numbers are a similar result, not an exact reproduction.

## Reproduction

1. Create a work folder with `scripts/` (copy `files/code/*.py`) and a `datasets` link next to the work folder (`../datasets` relative to the work folder) that contains the four shared inputs above.
2. Python 3.12 with numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, statsmodels 0.15.0, xarray 2026.9.0, netCDF4, matplotlib 3.11.2. Script 03 also needs `mapbox-vector-tile` 2.2.0 (we used a private virtual environment). Set `OMP_NUM_THREADS=1` on a loaded machine; the scripts set it by default.
3. Run in order: `01_prepare.py`, `02_site_weather.py`, `03_gbif_sti.py` (internet access, or unpack `files/raw/gbif_density_tiles_20261109.tar.gz` into `raw/` to use the archived tiles), `04_sample_table.py`, `05_indices.py`, `06_analysis.py`, `07_robustness.py`, `08_figures.py`. Total run time is about 10 minutes, most of it for the GBIF download.
4. Outputs go to `derived/`, `results/` and `figures/`. The bundle contains all of them in `files/derived`, `files/results` and `files/figures`. Bootstrap seeds are fixed.

Main derived files: `samples.csv` (transect-sample table with effort, temperature and zero-filled counts), `annual_index.csv` (O and E per taxon, site, year, raw and adjusted), `species_sti.csv` (GBIF match and STI), `species_cells.csv` (occupied cells), `activity_beta.csv` (temperature activity coefficients), `trends.csv` (all slopes).

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-climate-pollution-biodiversity-18878586d0e6, topic climate-pollution-biodiversity, machine dell, account claude-andrii.
- Analysis and text by the AI model Claude Opus 5.5 (claude-opus-5-5), working as an automated research worker. The signing key is a campaign-machine key. It is not a personal authorship claim.
- Analysis date: 2026-11-09. GBIF tiles retrieved on 2026-11-09.
