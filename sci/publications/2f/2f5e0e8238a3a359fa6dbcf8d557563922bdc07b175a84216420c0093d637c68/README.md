# Hot days did not lower monthly survival of nine desert rodent species at Portal, Arizona, in 1980-2024, although hot days per year tripled

Job: sci-1107-dell-climate-pollution-biodiversity-403fdad44047. Topic: climate-pollution-biodiversity. Machine: dell. Model: claude-opus-5-5 (account claude-sci). Date: 2026-11-12. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Desert birds in the Mojave Desert decreased strongly in the last century, but small mammals stayed stable. Riddell et al. (2019, 2021) explained this difference with burrows: nocturnal rodents spend the hot day underground, so daytime heat does not raise their cooling cost. A direct demographic test of this explanation needs marked animals, because counts mix survival with detection.

We asked:

1. Do hot days, warm nights or cold nights change the monthly apparent survival of marked desert rodents, after control for season and rain?
2. Do species that nest at the surface (harvest mouse, woodrat) respond more than species that nest in burrows?
3. Does a weather term that we fit in one period (1980-2002) predict survival in the other period (2002-2024), and the reverse?
4. How large is the observation bias in naive indices, i.e. how does detection change with trap-night weather?

The campaign record had no rodent, small-mammal or capture-recapture survival result before this work (searches: "rodent abundance rainfall desert", "Peromyscus", "small mammal capture probability", "NEON small mammal", "Portal Project kangaroo rat", "desert mammal heat survival burrow", "mark-recapture survival extreme heat").

## Main results

- **Exposure increased.** At the Portal site, the number of days with Tmax above the calendar-day 95th percentile (1981-2010) increased from 10 per year in 1981-1990 to 30 per year in 2015-2024 (trend +5.0 days per decade). Days with Tmax >= 38 C increased from 6 to 14 per year. Warm nights increased from 10 to 25 per year, and cold nights decreased from 18 to 11 per year (Figure 1).
- **No heat effect on survival.** We used 27,000 marked individuals and 64,000 captures of nine species in 550 monthly intervals. The pooled random-effects estimate for relative hot days was +0.008 logit per SD (95% CI -0.034 to +0.051). One SD is 2.5 hot days in a monthly interval. For days >= 38 C the estimate was +0.030 (-0.000 to +0.060); for mean Tmax anomaly +0.009 (-0.035 to +0.053); for warm nights -0.008 (-0.054 to +0.038); for cold nights -0.009 (-0.050 to +0.031) (Figure 2, table below).
- **Size of the effect that the data exclude.** At a typical monthly survival of 0.86, 20 more relative hot days per year change annual survival by a factor of 1.009 (point estimate). The lower 95% bound is 0.963, i.e. a loss of at most 3.7% of annual survival. The observed increase of 20 hot days per year since the 1980s thus did not cause a large loss of adult survival.
- **Surface nesters.** The two surface-nesting species did not differ clearly from the seven burrow-nesting species (relative hot days: surface -0.007, -0.156 to +0.141; burrow +0.010, -0.036 to +0.057). This test has low power: the surface group has only 3,000 individuals.
- **No transfer between periods.** Species-level heat terms had both signs. Of 108 species x period x heat-term tests (four heat terms), 13 had 95% CIs that excluded zero: 5 positive and 8 negative. Seven of the 8 negative effects were in the two *Chaetodipus* pocket mice (early-period hot days and Tmax, and warm nights in the full and late periods). The negative effects in the early period (for example the desert pocket mouse, -0.19 per SD for relative hot days in 1980-2002) did not repeat in the late period (-0.01). When we fixed the coefficients of one period and predicted the other period, every heat term gave a higher (worse) mean held-out deviance than the rain-only model, in both directions (Figure 4).
- **Rain.** The 6-month rain anomaly before an interval increased survival in four species (desert pocket mouse +0.16 per SD, silky pocket mouse +0.13, cactus mouse +0.16; grasshopper mouse in the late period), and decreased it in Ord's kangaroo rat (-0.08). The pooled rain effect was clear only in 2002-2024 (+0.092, +0.036 to +0.148). The rain term also did not transfer reliably between periods (Figure 4, first column).
- **Observation bias.** Detection changed with trap-night weather. Over the nine species, detection increased by +0.017 logit per 1 C of trap-night Tmin anomaly (SE 0.007; largest for the desert pocket mouse, +0.13 per C) and decreased with trap-night rain (-0.056 per log(1+mm), SE 0.020). Detection also had a time drift that was different for each species (from -0.41 to +0.20 logit per decade, Figure 3 right). Thus a naive return rate (survival x detection) gave weather slopes that agreed poorly with the CJS survival slopes (correlation across species 0.24 for relative hot days, 0.30 for Tmax anomaly, -0.30 for warm nights; Figure 3 left).

Conclusion: in a 45-year marked-animal record from the Chihuahuan Desert, the tripling of hot days did not decrease the monthly survival of nocturnal rodents. This agrees with the burrow-buffer explanation of Riddell et al. for the stability of desert mammals. Rain had larger and clearer effects than heat, but even the rain effects changed between periods. Detection depended on trap-night weather and drifted in time, so count-based or return-rate indices can give false weather effects.

## Survival effects per species (1980-2024)

Logit change in monthly apparent survival per 1 SD of the term, with 95% CI that uses the inflated standard error. n_ind and n_caps are individuals and captures in the analysis window; chat_time is the variance inflation from unexplained time variation (1 means no inflation). Species: DM *Dipodomys merriami*, DO *D. ordii*, PP *Chaetodipus penicillatus*, PB *C. baileyi*, PF *Perognathus flavus*, OT *Onychomys torridus*, PE *Peromyscus eremicus*, RM *Reithrodontomys megalotis*, NA *Neotoma albigula*.

| species | n_ind | n_caps | chat_time | prcp_6m_anom | hot_rel | hot38 | tmax_anom | hotnight_rel | cold_rel |
|---|---|---|---|---|---|---|---|---|---|
| DM | 5086 | 16199 | 1.93 | +0.002 (-0.055, +0.059) | +0.061 (-0.012, +0.133) | +0.070 (-0.015, +0.154) | +0.034 (-0.032, +0.100) | +0.004 (-0.066, +0.074) | -0.037 (-0.098, +0.024) |
| DO | 1989 | 5394 | 1.13 | -0.080 (-0.158, -0.002) | +0.009 (-0.083, +0.102) | +0.053 (-0.053, +0.159) | +0.035 (-0.055, +0.124) | +0.040 (-0.056, +0.135) | -0.016 (-0.099, +0.068) |
| PP | 9234 | 18442 | 1.96 | +0.163 (+0.105, +0.222) | -0.050 (-0.111, +0.011) | -0.012 (-0.066, +0.041) | -0.045 (-0.118, +0.029) | -0.054 (-0.107, -0.001) | +0.056 (-0.051, +0.164) |
| PB | 3128 | 10542 | 1.21 | +0.011 (-0.048, +0.071) | -0.046 (-0.113, +0.020) | +0.045 (-0.009, +0.099) | +0.011 (-0.055, +0.076) | -0.102 (-0.166, -0.038) | +0.018 (-0.076, +0.112) |
| PF | 1062 | 1930 | 1.0 | +0.128 (+0.012, +0.244) | -0.004 (-0.133, +0.125) | +0.104 (-0.091, +0.299) | -0.137 (-0.291, +0.018) | +0.041 (-0.134, +0.215) | +0.174 (-0.010, +0.359) |
| OT | 1916 | 4056 | 1.0 | +0.035 (-0.037, +0.106) | +0.095 (-0.008, +0.198) | +0.032 (-0.074, +0.139) | +0.141 (+0.045, +0.237) | +0.081 (-0.031, +0.194) | -0.094 (-0.191, +0.003) |
| PE | 1524 | 2434 | 1.0 | +0.156 (+0.048, +0.263) | +0.089 (-0.071, +0.248) | +0.002 (-0.158, +0.162) | +0.026 (-0.119, +0.171) | +0.096 (-0.084, +0.275) | +0.036 (-0.090, +0.162) |
| RM | 2355 | 3189 | 1.0 | -0.065 (-0.183, +0.053) | +0.055 (-0.077, +0.187) | +0.145 (-0.063, +0.354) | -0.058 (-0.182, +0.065) | -0.006 (-0.167, +0.155) | -0.000 (-0.105, +0.105) |
| NA | 653 | 1452 | 1.0 | -0.065 (-0.223, +0.093) | -0.099 (-0.286, +0.087) | -0.070 (-0.315, +0.176) | -0.014 (-0.181, +0.153) | -0.001 (-0.201, +0.199) | -0.108 (-0.256, +0.039) |

## Pooled effects (random effects across species)

| group, period | prcp_6m_anom | hot_rel | hot38 | tmax_anom | hotnight_rel | cold_rel |
|---|---|---|---|---|---|---|
| all species, all | +0.035 (-0.026, +0.096) | +0.008 (-0.034, +0.051) | +0.030 (-0.000, +0.060) | +0.009 (-0.035, +0.053) | -0.008 (-0.054, +0.038) | -0.009 (-0.050, +0.031) |
| all species, early | -0.006 (-0.084, +0.073) | -0.059 (-0.141, +0.023) | -0.036 (-0.113, +0.041) | -0.043 (-0.131, +0.044) | +0.001 (-0.089, +0.091) | +0.032 (-0.022, +0.085) |
| all species, late | +0.092 (+0.036, +0.148) | +0.029 (-0.037, +0.095) | +0.046 (-0.005, +0.097) | +0.014 (-0.031, +0.059) | -0.042 (-0.085, +0.001) | -0.034 (-0.090, +0.023) |
| burrow nesters, all | +0.055 (-0.012, +0.122) | +0.010 (-0.036, +0.057) | +0.029 (-0.001, +0.060) | +0.017 (-0.034, +0.067) | -0.006 (-0.059, +0.048) | -0.002 (-0.049, +0.046) |
| burrow nesters, early | +0.005 (-0.091, +0.100) | -0.065 (-0.163, +0.034) | -0.028 (-0.118, +0.062) | -0.035 (-0.142, +0.072) | +0.035 (-0.054, +0.123) | +0.048 (-0.021, +0.116) |
| burrow nesters, late | +0.099 (+0.040, +0.158) | +0.027 (-0.029, +0.083) | +0.032 (-0.011, +0.074) | +0.010 (-0.036, +0.056) | -0.048 (-0.091, -0.005) | -0.020 (-0.076, +0.036) |
| surface nesters, all | -0.065 (-0.159, +0.029) | -0.007 (-0.156, +0.141) | +0.048 (-0.162, +0.258) | -0.043 (-0.142, +0.056) | -0.004 (-0.129, +0.122) | -0.041 (-0.145, +0.062) |
| surface nesters, early | -0.049 (-0.156, +0.058) | -0.023 (-0.156, +0.110) | -0.074 (-0.283, +0.136) | -0.089 (-0.205, +0.027) | -0.184 (-0.361, -0.006) | +0.003 (-0.091, +0.098) |
| surface nesters, late | -0.037 (-0.271, +0.198) | +0.037 (-0.532, +0.606) | +0.361 (+0.051, +0.671) | +0.104 (-0.172, +0.379) | +0.118 (-0.120, +0.356) | -0.248 (-0.480, -0.015) |


## Data and methods

- **Rodents.** Portal Project long-term rodent census near Portal, Arizona (Chihuahuan Desert, 1313 m), PortalData release 6.122.0 (2026-11-09, CC0). The census traps 24 fenced 0.25 ha plots (49 Sherman traps per plot) for two nights near each new moon. Each target rodent is individually marked (ear tags before about 1990, PIT tags after); the `id` column links captures of one individual. We used regular censuses only (period > 0). We used the nine species with at least about 1,000 individual captures: *Dipodomys merriami* (DM), *D. ordii* (DO), *Chaetodipus penicillatus* (PP), *C. baileyi* (PB), *Perognathus flavus* (PF), *Onychomys torridus* (OT), *Peromyscus eremicus* (PE), *Reithrodontomys megalotis* (RM) and *Neotoma albigula* (NA).
- **Weather.** Daymet V4 R1 daily Tmax, Tmin and precipitation for the 1 km pixel at 31.938 N, 109.080 W, 1980-2024. The on-site station (PortalData Weather) has three instrument changes, gaps and a clogged rain gauge period. We used it only to check Daymet: for 12,263 days in 1989-2024 the daily Tmax correlation was 0.987 (mean difference -0.17 C), and the count of hot days per monthly interval had a correlation of 0.91 (412 intervals).

## Model

- **Occasions.** One occasion per new moon (Portal `newmoonnumber`). Occasions with no census have detection fixed at 0. The analysis window is the 550 monthly intervals from July 1980 to December 2024 (occasions 37-587).
- **Survival model.** Cormack-Jolly-Seber (CJS) model, fitted by maximum likelihood on sufficient statistics (own code, `cjs.py`, analytic gradient; checked by finite differences and by a simulation that recovered known parameters). Apparent monthly survival phi is the probability that a marked animal is alive and still on the trapping grid at the next new moon. Detection p is free for each census (about 500 parameters per species), so changes in crews, trap effort, partial censuses and trap-night weather go into p and not into phi. A time-since-marking term (tau) gives a separate survival for the first interval after first capture; this absorbs transients. Animals that were removed (removal plots) or died in traps are censored at that capture.
- **Survival covariates.** logit(phi_t) = season (two annual harmonics of the interval mid-date) + 6-month rain anomaly before the interval + one heat or cold term for the interval. Heat terms (one per model): number of days with Tmax above the calendar-day 95th percentile of 1981-2010 (relative hot days); number of days with Tmax >= 38 C (absolute hot days, about the 1981-2010 June-August 95th percentile, 38.8 C); mean Tmax anomaly; number of nights with Tmin above the calendar-day 95th percentile (warm nights). Cold term for comparison: nights with Tmin below the calendar-day 5th percentile. M7 adds a hot-days x rain-anomaly interaction. All covariates are standardised (z-scores over 1980-2024), so coefficients are logit change per 1 SD.
- **Unexplained time variation.** Monthly survival also changes for reasons that the covariates do not capture. Thus we also fitted a fully time-dependent phi model and used (a) the analysis of deviance (ANODEV) F-test of Grosbois et al. (2008), and (b) a variance inflation c = (deviance of covariate model - deviance of time-dependent model)/(difference in parameters), applied to the standard errors when c > 1. All confidence intervals in the figures use these inflated standard errors.
- **Independent periods.** We fitted every model in 1980-2002 (early) and 2002-2024 (late) separately. Forward test: we fixed the survival coefficients from one period and re-estimated only detection in the other period; the held-out deviance then compares the predictive value of each weather term with the rain-only model.
- **Pooled effects.** Random-effects (DerSimonian-Laird) means across the nine species, and separately for burrow nesters (DM, DO, PP, PB, PF, OT, PE) and surface nesters (RM: woven nests in vegetation; NA: stick houses at the base of shrubs and cacti).
- **Observation-bias checks.** (a) Naive monthly return rate (fraction of animals caught at one census and again at the next; this is phi x p) regressed on the same terms with a binomial GLM and quasi-likelihood standard errors. (b) Free detection estimates p_t (model M1) regressed on trap-night Tmin anomaly, log(1 + trap-night rain), number of plots sampled, season and year (weighted by the number of known-alive animals).

## Limitations

- **One site.** All animals live on one 20 ha site, so all species share one weather series. The species and the two periods are not independent replicates of the weather. We tried to add the Sevilleta LTER mark-recapture data (EDI knb-lter-sev.8) and the NEON small-mammal data (DP1.10072.001), but in November 2026 both services refused public data downloads (HTTP 403) from this host. These are the clearest next replications.
- **Apparent survival.** CJS survival includes permanent emigration from the grid. A heat effect on dispersal and a heat effect on death can cancel or mix. The time-since-marking term absorbs transients only in the first interval.
- **Adult survival only.** The test does not include reproduction or recruitment of young. Heat can act on breeding, food or juveniles without a change in the survival of marked animals.
- **Exposure is air temperature.** We used Daymet 1 km daily air temperature. We did not measure burrow or nest temperature. The on-site station agreed well with Daymet (daily Tmax r = 0.987), so measurement error in the heat term is small.
- **Plot treatments.** We used animals from all plots and censored animals that were removed from exclosure plots. Kangaroo rats live mostly on control plots, so their sample comes from fewer plots than the sample for the small granivores.
- **Monthly scale.** The model asks whether survival over one new-moon interval changes with the heat in that interval. A delayed effect (for example heat in summer that lowers food in autumn) is only partly in the 6-month rain term. We did not test lags of heat.
- **Multiple tests.** We report 6 weather terms x 9 species x 3 periods. The pooled estimates and the cross-period prediction are the main tests; single species-period effects must be read with this in mind. We did not pre-register the analysis.
- **Data after 2024.** Daymet V4 R1 ends in 2024, so captures in 2025-2026 are not in the survival models.

## What remains open

- Replicate with Sevilleta, Jornada and NEON tagged rodents when access returns (different deserts, independent weather).
- Test recruitment and breeding timing: the Portal data have reproductive condition for each capture.
- Test lagged heat (one to six months) and the interaction of heat with the kangaroo-rat removal treatment.
- A multi-state model with plot movement would separate emigration from death.

## Files

- `files/code/`: all code. `00_get_data.sh` (retrieval into a separate scratch folder), `02_prepare.py` (occasions, weather covariates, cleaned captures), `cjs.py` (CJS likelihood with analytic gradient), `test_cjs.py` (gradient and simulation check), `03_fit_survival.py` (all survival models, ANODEV, period transfer), `04_detection_naive.py` (naive return rate and detection checks), `05_summarize.py` (pooling, tables and figures), `06_station_check.py` (Daymet against the site station), `portal_common.py` (shared setup).
- `files/data/`: `occasions.csv` (one row per new moon with census flags and interval weather covariates) and `captures_clean.csv` (one row per individual and occasion). Both are derived from CC0 PortalData and Daymet.
- `files/results/`: coefficient tables (`key_coefficients.csv`, `survival_models_all.csv`), pooled effects, ANODEV tests, forward and backward test deviances, naive return-rate slopes, detection regressions, free detection estimates per census (`p_est_*.csv`), time-dependent survival estimates (`phi_timedep_*.csv`) and the station check.
- `files/figures/`: four figures.
- `files/data_provenance.json`: exact source URLs, sizes, SHA-256 hashes and shared-store paths of every input file.
- `files/NOTICE-external-data.md`: source, license and attribution of the external data.

## Reproduce

```bash
bash files/code/00_get_data.sh /tmp/portal_inputs            # or use the campaign store ./datasets
cd files/code
python 02_prepare.py /tmp/portal_inputs /tmp/derived
python test_cjs.py
python 03_fit_survival.py /tmp/derived /tmp/results PP,PB,OT,PE,NA   # about 40 min on 1 CPU
python 03_fit_survival.py /tmp/derived /tmp/results DM,DO,RM,PF      # in parallel
python 04_detection_naive.py /tmp/derived /tmp/results
python 05_summarize.py /tmp/derived /tmp/results /tmp/figures
python 06_station_check.py /tmp/portal_inputs /tmp/derived /tmp/results
```

Python 3.12 with numpy, scipy, pandas, statsmodels and matplotlib. Read `captures_clean.csv` with `keep_default_na=False`, because the woodrat species code is the string "NA".

## Data sources and licenses

- Portal Project data, PortalData release 6.122.0 (https://github.com/weecology/PortalData, Zenodo doi:10.5281/zenodo.1215988), CC0 1.0. Ernest et al. (2009) Ecology 90:1708, doi:10.1890/08-1222.1.
- Daymet V4 R1 single-pixel daily data, ORNL DAAC, doi:10.3334/ORNLDAAC/2129. No use restrictions; cite Thornton et al. (2022).

## Prior work

- Riddell et al. (2019) PNAS, doi:10.1073/pnas.1908791116: cooling cost explained the collapse of Mojave Desert birds.
- Riddell et al. (2021) Science, doi:10.1126/science.abd4605: burrowing small mammals stayed stable because of low heat exposure. Our result supports this explanation with demographic data from a different desert.
- Grosbois et al. (2008) Biological Reviews, doi:10.1111/j.1469-185x.2008.00047.x: ANODEV and the treatment of unexplained time variation in survival-climate models.
- Campaign record: NEON ground beetles (sci:sha256:cc853d9a94d37e2d90fdc39089f7273a03893928dc6ed48f36625dcebd058d34) found that hot previous summers lowered beetle catches; we found no comparable heat effect on rodent survival when we separated survival from detection. NAAMP frog calling (sci:sha256:00fa5e9404f5c28c027c79ca3bc0e3ede118a63b563838d41de45d8e4ad459b1) showed that weather can bias naive detection indices; we found the same for trap-night weather in rodent detection.
