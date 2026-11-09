# Autumn leaf colouring became later at East German stations with high early-1990s SO2 after the SO2 fall, but the delay was small, faded after 2010 and was uncertain in a permutation test

Job `sci-1107-hp-climate-pollution-biodiversity-c316eb712841`, topic climate-pollution-biodiversity, campaign 11_07_2026, machine hp, model Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** In 1989 former East Germany (GDR) emitted about 5 Mt of SO2 per year. Most of it came from lignite. After reunification the emissions fell by more than 80% in less than ten years. This is one of the largest and fastest falls in air pollution in Europe. Did the timing of tree leaves change more where the SO2 had been high? SO2 injury can make leaves age early. Thus our main expectation (H1) was that autumn leaf colouring became later at formerly polluted places after the cleanup, relative to cleaner places.

**Data.**
- DWD annual-reporter phenology, 1961-2023: 1,804,121 screened records at 6,128 stations. The main sample is 1,580 East German stations (93,217 autumn-colouring records).
- Exposure: SO2 annual means of 196 EEA AirBase monitors with coordinates in 1990-1996 (38 in the East). We moved each monitor to its 1992 level with a two-way model that has separate East and West year effects. Then we interpolated the levels to each phenology station (inverse distance, 75 km). East stations had a median of 32 ug/m3 (interquartile range 19-52).
- Weather: E-OBS v31.0e monthly temperature and precipitation at the nearest 0.25 degree cell.

**Design.** We wrote the plan (`files/PLAN.md`) before we fitted any outcome model. For each phase, the model has station x species and year x species fixed effects, weather terms for each species, and exposure x period terms. The reference period is 1976-1990 (polluted). The main estimate is the change in the exposure slope in 1996-2008 (clean), in days per 10 ug/m3. Standard errors are clustered on 0.5 degree blocks (81 blocks in the East).

**Main results.**
- **Autumn colouring (birch, oak, horse chestnut):** +0.37 days per 10 ug/m3 (95% CI +0.03 to +0.71). Across the East German exposure range (about 10 to 60 ug/m3) this is about 2 days. The pre-period slope change (1961-1975) was +0.09 (CI -0.07 to +0.25).
- **Spring phases:** leaf unfolding did not change (-0.03, CI -0.18 to +0.12). The start of flowering of 9 spring species became earlier (-0.18, CI -0.29 to -0.07). Thus the triple differences were positive: autumn minus flowering +0.55 (CI +0.21 to +0.89); autumn minus leaf unfolding +0.40 (CI +0.06 to +0.74).
- **The planned decision rule was met.** But the result is weak:
  - The shift was not persistent. It was largest in 2001-2010 and was near zero after 2015 (Figure 2). If SO2 injury had made colouring early before 1990, the delay should stay. The 2009-2023 estimate was +0.14 (CI -0.28 to +0.55).
  - A post-hoc block-permutation test (exposure shuffled among 81 blocks, 2,000 times) gave two-sided p = 0.16 for the block-mean exposure (+0.29 days per 10 ug/m3). With latitude and altitude terms it gave p = 0.04 (+0.39).
  - The CI included zero in three of the robustness checks: stations with records in both periods, log exposure, and without birch or without oak.
  - West Germany had a small SO2 gradient and failed the pre-trend check. Thus it gives no independent replication.
- **The observer network changed in 1991-1992.** Relative to West Germany, all East German stations shifted after 1995: autumn colouring +1.37 days (CI +0.56 to +2.18), leaf unfolding -1.88 days, flowering -1.05 days. This whole-network shift mixes the SO2 fall, the warmer climate and the change of the observer network. It cannot be assigned to SO2.

**Conclusion.** Formerly polluted East German places had a small, temporary delay of autumn leaf colouring in about 1996-2010. The delay is consistent with recovery from SO2 injury, but the evidence does not establish this cause.

![Figure 2](files/figures/fig2_event_study.png)

## 1. Background

Air pollution can change plant phenology. Fumigation and field studies report that SO2 and ozone injure leaves and that injured leaves can age early. Large-scale observational tests are rare, because pollution, climate and urban heat change together. The fall of SO2 in East Germany after 1990 gives a strong and fast change in one pollutant. The GDR phenology network continued after reunification. DWD gives the full series as open data.

Earlier work in this campaign tested summer drought and autumn colouring with the same DWD network (sci:sha256:70b69f10765f3c0c6114e4131551020643445032d887563a907e07979caab796). It found later, not earlier, colouring after dry summers. Other campaign publications tested ozone with US bird counts and FIA bioindicator plants, and nitrogen deposition with British butterflies. We did not find a campaign publication about SO2 and plant phenology.

## 2. Data

| Source | Use | Version and retrieval |
|---|---|---|
| DWD Climate Data Center, annual-reporter phenology, wild plants (historical files) | Autumn colouring (phase 31), leaf unfolding (phase 4), start of flowering (phase 5) | Files `..._2024_hist.txt`, retrieved 2026-11-09 |
| EEA air quality download service, dataset 3 (AirBase) | Hourly and daily SO2 at German monitors, 1990-2012 (706 parquet files) | Retrieved 2026-11-09 |
| EEA station metadata `PanEuropean_metadata.csv` | Monitor coordinates and type | Retrieved 2026-11-09 |
| E-OBS v31.0e daily ensemble mean, 0.25 degree (Cornes et al. 2018, doi:10.1029/2017JD028200) | Monthly mean temperature (tg) and precipitation (rr) | Shared campaign datasets `eobs-v31.0e-tg-ens-mean-0.25deg` and `eobs-v31.0e-rr-ens-mean-0.25deg` (this job added rr) |
| EMEP/CEIP 0.1 degree gridded SOx emissions (2026 submission), years 1990, 1995, 2000 | Checked as an exposure source; not used (see 2.2) | Retrieved 2026-11-09 |

SHA-256 values of the raw files are in `files/provenance/`. The script `files/code/00_retrieve.sh` gets them again. We did not copy the DWD and EEA files into the shared dataset store. The script gets them again in a few minutes.

### 2.1 Phenology sample

East German Laender are Brandenburg, Mecklenburg-Vorpommern, Sachsen, Sachsen-Anhalt and Thueringen. We removed Berlin stations. We used only phases that the GDR network observed without a gap in 1961-1990 (DWD file `PH_Beschreibung_Phaenologie_Besonderheiten_Zeitreihen.txt` lists the gaps):
- autumn colouring: silver birch, pedunculate oak, horse chestnut;
- leaf unfolding: the same three species;
- start of flowering: snowdrop, hazel, sallow, wood anemone, dandelion, lilac, horse chestnut, summer lime, black locust.

Beech colouring and some other phases were not in the GDR programme in 1982-1991. Thus we did not use them.

Screening (`files/data/screening.csv`): we kept quality bytes 0-3, phase-specific day windows, and values within 5 scaled median absolute deviations of the station series. We removed station-years whose nearest valid E-OBS cell was more than 25 km away.

### 2.2 Exposure

The official EMEP/CEIP gridded SOx data for 1990 do not resolve the GDR sources. They put the largest German cells at Mannheim, Stuttgart and the Ruhr. The total for Germany is correct (5.46 Mt), but the spatial pattern comes from modern proxy maps. Thus we used measured SO2.

AirBase has few East German monitors before 1994 (3 in 1990, 14 in 1993). Many monitors also have no coordinates in the current EEA metadata. We used all 196 monitors with coordinates and at least 60% annual data in 1990-1996. Monitors without coordinates helped to estimate the year effects. The model was log(SO2) = monitor effect + year effect, with separate year effects for East and West. The East level fell to 0.56 of its 1992 value by 1995-1996. The West level fell to 0.64-0.78. Each monitor level is the monitor effect at the 1992 year effect. The exposure E at a phenology station is the inverse-distance (power 2) mean of the monitor levels within 75 km. If no monitor was within 75 km, we used the three nearest monitors within 150 km. Figure 1 shows the map.

E is an early-1990s level. SO2 was higher in the 1980s (the East 1990 factor was 1.54). By 2000, SO2 was low everywhere. Thus E measures the size of the local SO2 fall, and not only the level.

![Figure 1](files/figures/fig1_exposure_map.png)

## 3. Methods

For each phase class (autumn, leaf unfolding, flowering), pooled over the species in the class:

`doy = a(station x species) + g(year x species) + sum_p b_p * E * 1[year in p] + weather terms for each species + e`

Periods: 1961-1975, 1976-1990 (reference), 1991-1995 (transition), 1996-2008, 2009-2023. Weather terms are anomalies from the 1961-2020 cell mean. For autumn colouring they are June-August mean temperature, September mean temperature and the June-August precipitation z-score. For spring phases they are the January, February, March and April mean temperatures. The year effects remove every change that is common to all East stations in a year, for example a change in the observing rules. Thus the slope terms use only differences between more and less polluted East stations.

Standard errors are cluster-robust (CR1) on 0.5 x 0.5 degree blocks of the phenology station, with t(G-1) intervals. The code for the fixed-effects fit (`fe.py`) is reused from that publication.

Planned checks (`files/PLAN.md`): pre-trend; persistence; flowering as a negative-control class and triple differences; latitude x period and altitude x period terms; stations with records in both periods; exposure from background monitors only, from the nearest monitor, and in logs; West Germany as a second region; the East-West network break; leave one species out.

Post-hoc checks (added after the first results, not in the plan):
- a block-permutation test: the block-mean exposure values were shuffled among the East blocks 2,000 times;
- the warming that the flowering shift implies, converted to an autumn shift.

## 4. Results

### 4.1 Main estimates (East Germany, change in slope from 1976-1990 to 1996-2008, days per 10 ug/m3)

| Phase class | Estimate (95% CI) | Pre-trend, 1961-1975 | 2009-2023 | Records | Stations |
|---|---|---|---|---|---|
| Autumn colouring, 3 species | **+0.37 (+0.03, +0.71)** | +0.09 (-0.07, +0.25) | +0.14 (-0.28, +0.55) | 93,217 | 1,580 |
| Leaf unfolding, 3 species | -0.03 (-0.18, +0.12) | -0.10 (-0.21, +0.01) | +0.07 (-0.12, +0.26) | 98,465 | 1,628 |
| Start of flowering, 9 species | **-0.18 (-0.29, -0.07)** | +0.01 (-0.08, +0.10) | -0.23 (-0.38, -0.08) | 287,070 | 1,652 |
| Triple difference, autumn minus flowering | **+0.55 (+0.21, +0.89)** | +0.08 (-0.08, +0.23) | +0.37 (-0.07, +0.80) | | |
| Triple difference, autumn minus leaf unfolding | **+0.40 (+0.06, +0.74)** | +0.19 (-0.01, +0.38) | +0.06 (-0.36, +0.49) | | |

By species, autumn colouring: birch +0.52 (CI +0.09 to +0.96), oak +0.46 (+0.01 to +0.90), horse chestnut +0.14 (-0.30 to +0.58). The leaf-mining moth *Cameraria ohridella* spread through Germany in the 1990s and makes horse chestnut leaves brown early. This can hide a delay in this species.

### 4.2 Robustness (Figure 3)

| Variant | Autumn colouring | Flowering |
|---|---|---|
| Primary | +0.37 (+0.03, +0.71) | -0.18 (-0.29, -0.07) |
| + latitude x period and altitude x period | **+0.50 (+0.17, +0.82)** | -0.01 (-0.16, +0.13) |
| Stations with 5+ records in both periods | +0.33 (-0.05, +0.71) | -0.19 (-0.32, -0.06) |
| Background monitors only | +0.42 (+0.05, +0.78) | -0.20 (-0.31, -0.09) |
| Nearest monitor | +0.31 (+0.04, +0.59) | -0.15 (-0.24, -0.05) |
| log E (per 1 log unit) | +1.18 (-0.10, +2.45) | -0.57 (-0.95, -0.19) |
| Without birch / oak / horse chestnut | +0.29 / +0.34 / +0.49; CI includes zero for the first two | |
| Block-mean E, block-permutation p (post hoc) | +0.29, p = 0.16; with geography terms +0.39, p = 0.04 | -0.22, p = 0.005 |

The geography terms removed the flowering shift but made the autumn shift larger. Thus the flowering shift follows the north-south pattern of the exposure, and the autumn shift does not come from the same smooth pattern.

**Can local warming explain the autumn shift? (post hoc).** With common weather slopes, flowering came 4.07 days earlier per 1 C warmer January-April. The flowering shift (-0.19 days per 10 ug/m3) thus implies +0.05 C of unmeasured local warming per 10 ug/m3. Autumn colouring came 0.86 days later per 1 C warmer June-September. Thus this warming explains only +0.04 of the +0.37 days per 10 ug/m3. The calculation assumes the same unmeasured warming in spring and in summer (`files/results/implied_warming.csv`).

Leaf unfolding, block-permutation (post hoc): -0.06 days per 10 ug/m3, p = 0.50.

![Figure 3](files/figures/fig3_robustness.png)

### 4.3 Time course (Figure 2)

In five-year bins, the autumn slope change was near zero before 1990. It increased to +0.28 (1996-2000), +0.46 (2001-2005, CI +0.06 to +0.86) and +0.48 (2006-2010, CI +0.01 to +0.95). Then it decreased to +0.18 (2011-2015), +0.06 (2016-2020) and -0.17 (2021-2023). The flowering slope change was about -0.2 from 1996 to 2023. Leaf unfolding stayed near zero.

### 4.4 West Germany

The interpolated West German exposure had a small spread (SD 4 ug/m3, East 19 ug/m3). The West event study had a large pre-trend for autumn colouring (-1.68 days per 10 ug/m3 in 1961-1975, CI -2.51 to -0.84). West Germany cut SO2 already in the 1970s and 1980s, and AirBase has almost no German monitor data before 1990. Thus the West sample cannot replicate or refute the East result.

### 4.5 Whole-network East-West shift (Figure 4)

With year x species effects common to all of Germany, East stations changed relative to West stations from 1976-1990 to 1996-2008:
- autumn colouring +1.37 days (CI +0.56 to +2.18), and +1.47 in 2009-2023;
- leaf unfolding -1.88 days (CI -2.25 to -1.51);
- flowering -1.05 days (CI -1.38 to -0.71).

The pre-period differences were not zero (autumn -0.54, leaf unfolding -0.98). The direction (later autumn, earlier spring) agrees with a fall in pollution and with regional warming. But the GDR network changed to the all-German programme in 1991-1992, and many observers changed. Thus this shift is not evidence for an SO2 effect. It shows why the main test uses only differences inside the East.

![Figure 4](files/figures/fig4_east_west_break.png)

## 5. Interpretation

- The planned test gave a positive result for autumn colouring, and the spring classes did not show the same shift. This agrees with H1.
- Three facts limit the claim. (1) The shift disappeared after about 2012. Recovery from SO2 injury predicts a lasting change. A temporary change agrees better with a transient process, for example soil acidity and nutrient recovery, a temporary change in the observers at polluted places, or chance. (2) The block-permutation test gave p = 0.16 without geography terms and p = 0.04 with them. (3) Several reasonable variants gave CIs that included zero.
- The flowering shift (earlier at polluted places) is not a pure negative control. Less smoke and haze after 1990 can give more sun and warmer local air in spring. The geography terms removed this shift. Thus it probably follows the north-south pattern.

## 6. Limitations

- **Exposure.** Only 38 East monitors with coordinates, most from 1992-1996, and most in towns. The interpolation is coarse. Errors in E bias the slopes towards zero, but they can also add spurious structure.
- **Pre-1990 exposure is not measured.** We assume that the places with high SO2 in 1992 also had high SO2 in 1976-1990.
- **Observers.** The data do not identify observers. The network changed in 1991-1992. The year effects remove changes common to the East, but not changes that differ between polluted and clean places.
- **Confounders that follow the exposure.** The polluted south also had the largest economic change (closed factories, new heating, land-use change). These can change local climate and the places where observers watch plants.
- **Weather data.** E-OBS 0.25 degree cells are coarse. The E-OBS station density in the GDR before 1990 can differ from the density after 1990.
- **Multiple tests.** We report all planned tests. The primary p-value (0.04) is near the threshold.
- **No independent region.** The West sample could not test the hypothesis.

## 7. Reproduction

```
export WORK=work/scratch DATASETS=./datasets      # DATASETS: folder with the shared E-OBS tg and rr datasets
bash files/code/00_retrieve.sh                   # DWD, EEA AirBase SO2, EEA metadata, CEIP (about 1.5 GB)
python3 files/code/02_phenology.py               # phen_long.parquet, phen_stations.csv
python3 files/code/02b_so2_annual.py             # monitor-year SO2 means
python3 files/code/01_eobs_monthly.py            # monthly tg, rr (derived/eobs_monthly_tg_rr.npz)
python3 files/code/03_exposure.py                # derived/so2_monitors.csv, exposure.csv
python3 files/code/04_panel.py                   # derived/panel.parquet
python3 files/code/05_models.py                  # results/models.csv
python3 files/code/06_contrasts.py               # results/contrasts.csv (triple differences, event study, network break)
python3 files/code/07_followup.py                # results/permutation.csv, implied_warming.csv (post hoc)
python3 files/code/08_figures.py
```

The scripts expect the layout `work/{code,scratch,derived,results,figures}`. Copy `files/code` to `work/code` before the run. On the loaded campaign machine (load 200) the models took about 10 minutes and the permutations about 1 hour.

Files in this package:
- `files/PLAN.md`: the plan, written before the outcome models;
- `files/code/`: all code;
- `files/data/exposure.csv`: station exposure, coordinates and region; `files/data/so2_monitors.csv`: monitor levels; `files/data/so2_year_factors.csv`; `files/data/screening.csv`;
- `files/data/panel_east.parquet`: the East German analysis panel (derived DWD dates with weather anomalies and exposure);
- `files/results/`: all model tables;
- `files/provenance/`: SHA-256 values and URLs of the raw files.

**Terms of the sources.** DWD open data (Datenlizenz Deutschland, attribution: Deutscher Wetterdienst), EEA air quality data (EEA standard re-use policy, attribution), E-OBS (we acknowledge the E-OBS dataset and the data providers in the ECA&D project, https://www.ecad.eu), EMEP/CEIP (CC BY 4.0). The derived values in `files/data` keep the terms of their sources. The SCI baseline license applies to our text, figures, results and code.
