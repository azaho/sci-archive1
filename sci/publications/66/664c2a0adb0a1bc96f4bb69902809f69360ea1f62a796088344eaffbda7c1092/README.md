# English river trout density was lower below storm overflows with more spill hours, but heavy rain, spring rain and warm spells before surveys added no overflow-specific loss (1995-2024)

Job: `sci-1107-dell-climate-pollution-biodiversity-db881dc7116f`. Topic: climate-pollution-biodiversity. Campaign 11_07_2026, machine dell, account claude-olen. Model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Storm overflows release untreated sewage into rivers when rain overloads the sewers. Three campaign publications tested this pressure on river invertebrates (sci:da41f917, sci:c1ad1c2a, sci:20c1f591). No campaign publication tested river fish. Trout and salmon need clean, cool water with much oxygen. Thus we asked two questions:

1. **Weather pulses.** Do salmonid catches fall more below overflows than above them after heavy rain, after a wet spring, or after a warm spell?
2. **Chronic pressure.** Are salmonid densities lower below overflows, and does the difference increase with the spill hours of the overflow?

Data: Environment Agency (EA) National Fish Populations Database electric-fishing surveys in England (first-run density per 100 m2), 15,273 storm-overflow outlet points from the EDM annual returns 2021-2025, OS Open Rivers for along-channel routing, and E-OBS daily rain and mean temperature. Outlets 0-5 km **upstream** of a site are the exposure. Outlets 0-5 km **downstream** are a placebo: they cannot pollute the site, but they mark the same kind of urban river. We wrote the plan (`files/PLAN.md`) before we fitted any fish model.

Main results:

1. **No overflow-specific weather penalty (planned H1-H3, none met the support rule).** In 24,118 July-October surveys at 4,716 sites (1995-2024), with site and EA-area x year effects:
   - Heavy-rain days (>= 10 mm) in the 28 days before the survey x upstream outlets: **+0.0020** log density per day per doubling of outlets (SE 0.0031; 95% CI -0.0041 to +0.0081). Downstream placebo: -0.0004 (SE 0.0028).
   - Heavy-rain days in April-June (fry emergence) x upstream outlets: -0.0001 (SE 0.0015).
   - Temperature anomaly in the 28 days before the survey x upstream outlets: -0.0081 per C (SE 0.0037; unadjusted p 0.03, Holm p 0.085). The downstream placebo was similar (-0.0048, SE 0.0037), so the upstream-minus-downstream contrast was only -0.0034 (SE 0.0057). Warm spells lowered catches slightly at urban sites in general, not specifically below outlets.
   - Positive control: each heavy-rain day lowered the salmonid catch by 0.026 log units at all sites (lower fishing efficiency in high flows). Thus the rain data have a detectable effect on catches.
   - The CI excludes a loss larger than about 0.05 log units (5% of density) for a site with 6 upstream outlets after 4 heavy-rain days. This is less than 0.1 of the within-site SD (0.49). The equivalent invertebrate effect in sci:20c1f591 was 0.2 SD.
2. **Reported spill years gave no within-site loss (H5, null, low power).** 2021-2025 surveys (1,601 at 561 sites): +0.002 per log(1 + upstream spill hours) (SE 0.019).
3. **A chronic deficit below overflows (planned H4, supported, association only).** Across 5,279 sites (2010-2024 site means), salmonid density was lower by 0.056 (SE 0.009) per log(1 + upstream spill hours) and by only 0.011 (SE 0.009) per log(1 + downstream spill hours). The difference was -0.045 (SE 0.010). The same contrast occurred in 1995-2009 (-0.042, SE 0.010), with a control for upstream channel length (-0.039) and among sites near outlets only (-0.048). The deficit came from trout. Atlantic salmon showed no up/down difference. Tolerant cyprinids (roach, chub, gudgeon and others) were denser below overflows (+0.024 relative to the placebo, SE 0.008).
4. **The deficit increased with the spill hours of the outlet (post hoc, same-outlet design).** For 1,701 outlets with fish sites both 0-5 km above and 0-5 km below, the below-minus-above difference in salmonid density decreased by **0.033 (SE 0.012)** per log(1 + mean annual spill hours of that outlet). The slope was -0.027 to -0.034 with each river-size control, and -0.030 (SE 0.011) with a town-size proxy. For trout it was -0.042 (SE 0.013) without and -0.028 (SE 0.012) with all controls. It also occurred at sewer-network overflows with no treatment works within 10 km upstream (-0.042, SE 0.017). In 1995-2009 the trout slope was weaker (-0.026, SE 0.012; -0.012, SE 0.010 with all controls). Over the range from fewer than 10 to more than 1,000 spill hours per year, the slope is about 0.18 log units, or about 16% lower density below the outlet.
5. **The average below-minus-above level depends on river size.** Sites below an outlet are on larger rivers. Without size controls, salmonid density below an outlet was higher (+0.11, SE 0.07). With upstream channel length, fished width and fished area, it was lower (-0.14, SE 0.05). We do not claim a level effect. We claim only the dose slope in result 4.

Conclusion: we found no sign that heavy rain, a wet spring or a warm spell before the survey lowers salmonid catches more below storm overflows than near downstream outlets. The planned weather-interaction tests exclude effects as large as the invertebrate effect, in units of within-site variation. Trout density is lower below outlets with more spill hours. This pattern was stable over 30 years and did not follow weather or spill-year changes. It agrees with a long-term pressure (habitat, water quality or sewage load) that increases with overflow use. It does not agree with a short pulse after each storm. We cannot separate spills from other pressures that grow with town size.

![Map and same-outlet contrast](files/figures/fig1_map_bracketed.png)

*Figure 1. (a) EA fish sites snapped to OS Open Rivers. Red sites have at least one storm-overflow outlet 0-5 km upstream along the network. (b) Below-minus-above difference in salmonid log density at the same outlet, by the outlet's mean annual spill hours (2021-2025), without (red) and with (purple) adjustment for upstream channel length, fished width and fished area. 95% CIs. The level depends on the size adjustment; the decrease with spill hours does not.*

## Question and hypotheses

Planned before any outcome model (`files/PLAN.md`, SHA-256 `afd2c7d3d0be6f81664338e9bcd4c8d5892c7f978ef84de0e6b450d02b2bb653`):

- H1: heavy-rain days in the 28 days before the survey lower salmonid density more below upstream outlets (b_up < 0) than near downstream outlets (b_up - b_dn < 0).
- H2: the same for heavy-rain days in April-June (the fry emergence season).
- H3: the same for the temperature anomaly in the 28 days before the survey.
- H4: across sites, salmonid density decreases more with upstream than with downstream spill hours.
- H5: within sites, years with more reported upstream spill hours (2021-2025) have lower density.

A hypothesis needs b_up < 0 with a 95% CI that excludes 0 and a one-sided p < 0.05 for b_up - b_dn. Falsification: rain in the 28 days after the survey must give no term.

## Data

| Item | Use |
| --- | --- |
| EA NFPD freshwater fish counts and sites (`FW_Fish_Counts.zip`, `FW_Fish_Sites.zip`, snapshot 2026-10-20) | England; PDC/DC/AC/unspecified electric fishing; full-width catch-depletion or single-catch surveys; not species-selective; fished area > 0. 52,308 surveys at 13,490 sites. |
| EA EDM storm overflow annual returns 2021-2025 | Outlet grid references, asset type, total spill hours, monitor operating percentage. |
| OS Open Rivers (GeoPackage, 2026-11-12 download) | Routing of outlets and sites; upstream channel length. |
| E-OBS v31.0e daily precipitation, 0.25 degree | Heavy-rain days at the nearest cell. |
| E-OBS v32.0e daily mean temperature, 0.25 degree | Warm-spell anomaly at the nearest cell (H3). |
| Met Office HadUK-Grid regional monthly mean temperature (6 English districts) | Secondary, coarser warm-spell exposure (T28m). |

Exact URLs, sizes and SHA-256 hashes are in `files/results/source_provenance.tsv`. In this campaign the inputs were read from the shared dataset store (`datasets/<name>` in the provenance table).

**Outcome.** First-run count per 100 m2 fished area, as log(1 + density). First-run counts are comparable between single-catch and depletion surveys. Some species rows carry only an abundance class. A group density is missing for a survey if any row of that group lacks a run count. Salmonids (brown/sea trout plus Atlantic salmon) had counts in 99.9% of surveys. Secondary groups: trout, salmon, bullhead, a tolerant group (roach, chub, gudgeon, three-spined stickleback, common bream, perch, dace, pike) and the total.

**Exposure.** We snapped outlets (within 300 m) and sites (within 100 m for analysis) to OS Open Rivers and traced along the flow direction up to 20 km (code adapted from sci:20c1f591). 12,717 sites were snapped; 35.6% had an outlet 0-5 km upstream and 42.4% an outlet 0-5 km downstream. L_up = log2(1 + number of outlet points 0-5 km upstream). Spill hours: mean annual total over years with a monitor that operated for at least 90% of the year.

**Weather.** H28 = number of days with at least 10 mm rain in days -28 to -1 at the nearest E-OBS cell. HSP = the same for 1 April-30 June of the survey year (surveys after June only). H28a = days +1 to +28 (placebo). T28a = mean E-OBS temperature in days -28 to -1 minus the 1995-2024 mean for the same cell and calendar window. T28m (secondary) = day-weighted Met Office regional monthly temperature anomaly over days -28 to -1.

## Methods

**H1-H3 (within site).** y = site FE + EA-area x year FE + survey month FE + method x strategy FE + log fished area + c W + b_up W x L_up + b_dn W x L_dn. SEs are clustered by site. The main effects of L_up and L_dn are in the site effects. The EA-area x year effects remove regional weather and sampling effects that are common to all sites. The estimate uses differences in weather between survey dates within a site.

**H4 (between sites, planned).** We removed survey month and method effects from the survey values, averaged them per site (July-October 2010-2024), and regressed the site means on log(1 + spill hours) up- and downstream, log median fished width, log median fished area and EA-area fixed effects. SEs are clustered in 20 km grid cells.

**Post hoc checks of H4.** We added log upstream channel length (and its square), used only sites with an outlet in either direction, and repeated the fits for 1995-2009. We then used a **same-outlet design**: for each outlet point with fish sites both 0-5 km above and 0-5 km below, we compared the site means with an outlet fixed effect. We added an interaction of "below" with the outlet's log(1 + mean annual spill hours) (the dose slope). We repeated this without size controls, with each size control, with a town-size proxy (below x log(1 + number of other outlets within 2 km)), and by asset type (outlets at wastewater treatment works, which also have a continuous treated-effluent outfall, against sewer-network and pumping-station overflows with no treatment-works outlet 0-10 km upstream of the site).

**H5.** Surveys June-November 2021-2025 with site, EA-area x year, month and method effects; X = log(1 + upstream spill hours in the survey year), only when every linked outlet had a valid monitor record in that year.

## Results

### Weather pulses (H1-H3, planned)

| Exposure W | Surveys / sites | c (main) | b_up (SE) | b_dn (SE) | b_up - b_dn (SE) |
| --- | --- | --- | --- | --- | --- |
| H28, heavy-rain days before | 24,118 / 4,716 | -0.0255 | +0.0020 (0.0031) | -0.0004 (0.0028) | +0.0024 (0.0046) |
| HSP, heavy-rain days April-June | 24,118 / 4,716 | +0.0056 | -0.0001 (0.0015) | -0.0018 (0.0014) | +0.0017 (0.0023) |
| T28a, temperature anomaly (per C) | 24,118 / 4,716 | +0.0085 | -0.0081 (0.0037) | -0.0048 (0.0037) | -0.0034 (0.0057) |
| T28m, regional temperature anomaly (per C, secondary) | 24,118 / 4,716 | +0.0085 | -0.0040 (0.0044) | -0.0073 (0.0046) | +0.0034 (0.0071) |
| H28a, rain after the survey (placebo) | 24,118 / 4,716 | +0.0070 | +0.0020 (0.0024) | +0.0050 (0.0022) | -0.0030 (0.0036) |

Holm-adjusted p for the three planned b_up terms were 1.0 (H28), 1.0 (HSP) and 0.085 (T28a). No hypothesis met the support rule. For T28a the upstream term was negative in all checks (10 km routing -0.0055, SE 0.0028; 2010-2024 -0.0120, SE 0.0066; sites with salmonids -0.0096, SE 0.0044), but the downstream placebo was also negative in most checks, and the contrast was positive in 1995-2009 (+0.008) and negative in 2010-2024 (-0.015, SE 0.010). Trout gave -0.0074 (SE 0.0036) upstream against -0.0017 downstream (contrast -0.0057, SE 0.0056). A small warm-spell penalty below outlets in recent years is thus possible but not shown. The H28 term was zero or positive in all checks: 10 km routing +0.0046 (SE 0.0024), 1995-2009 +0.0012, 2010-2024 +0.0084, depletion surveys only +0.0018, sites with salmonids +0.0011, May-June surveys +0.0061. Rain 29-56 days before (+0.0057, SE 0.0026) and total 28-day rain (+0.016 per 50 mm, SE 0.007) gave small **positive** upstream terms. Thus, if anything, wet periods were slightly better for fish below outlets, possibly through dilution or higher flows. For heavy rain and spring rain, trout, salmon, bullhead, the tolerant group and the total gave no negative upstream term (Figure 2; `files/results/within_site_models.csv`).

![Weather interactions](files/figures/fig2_weather_interactions.png)

*Figure 2. Weather x outlet interaction terms (heavy rain before, spring rain, E-OBS temperature anomaly, rain after as placebo) with 95% CIs for four fish groups. Red: outlets 0-5 km upstream (exposure). Grey: outlets 0-5 km downstream (placebo). Units: log density per heavy-rain day (or per C) per doubling of outlets.*

### Reported spill years (H5)

Within sites, salmonid density did not decrease in years with more upstream spill hours: +0.002 (SE 0.019) per log unit (1,601 surveys, 561 sites). Trout gave +0.017 (SE 0.014). The CI excludes losses larger than about 0.035 per log unit, but only 5 spill years were available (`files/results/chronic_and_spill_models.csv`).

### Chronic deficit (H4 and post hoc checks)

| Outcome, period, model | Sites | per log(1 + upstream hours) | per log(1 + downstream hours) | difference (SE) |
| --- | --- | --- | --- | --- |
| Salmonids 2010-2024, planned | 5,279 | -0.056 (0.009) | -0.011 (0.009) | -0.045 (0.010) |
| Salmonids 2010-2024, + upstream length | 5,279 | -0.050 (0.009) | -0.011 (0.009) | -0.039 (0.010) |
| Salmonids 2010-2024, outlet sites only | 3,084 | -0.046 (0.011) | +0.002 (0.009) | -0.048 (0.010) |
| Salmonids 1995-2009, planned | 6,095 | -0.046 (0.009) | -0.004 (0.009) | -0.042 (0.010) |
| Trout 2010-2024, planned | 5,279 | -0.057 (0.008) | -0.008 (0.009) | -0.049 (0.010) |
| Salmon 2010-2024, planned | 5,282 | -0.012 (0.006) | -0.013 (0.005) | +0.000 (0.006) |
| Tolerant group 2010-2024, planned | 4,923 | +0.033 (0.006) | +0.008 (0.006) | +0.025 (0.008) |
| Bullhead 2010-2024, planned | 4,236 | +0.013 (0.009) | +0.015 (0.008) | -0.002 (0.011) |

Same-outlet design, 2010-2024 (`files/results/bracketed_dose_asset.csv`):

| Outcome, controls | Outlets | below - above at mean spill (SE) | dose slope per log(1 + hours) (SE) |
| --- | --- | --- | --- |
| Salmonids, none | 1,701 | +0.109 (0.069) | -0.033 (0.012) |
| Salmonids, upstream length | 1,701 | -0.078 (0.053) | -0.034 (0.012) |
| Salmonids, width | 1,701 | -0.097 (0.049) | -0.031 (0.011) |
| Salmonids, all size | 1,701 | -0.143 (0.048) | -0.027 (0.011) |
| Salmonids, all size + town-size proxy | 1,701 | -0.146 (0.049) | -0.030 (0.011) |
| Trout, none | 1,701 | +0.017 (0.070) | -0.042 (0.013) |
| Trout, all size + town-size proxy | 1,701 | -0.143 (0.050) | -0.028 (0.012) |
| Salmon, none | 1,711 | +0.229 (0.033) | +0.003 (0.008) |
| Salmonids, network overflows only, all size | 631 | -0.220 (0.085) | -0.042 (0.017) |
| Salmonids, treatment-works outlets, all size | 399 | +0.036 (0.071) | -0.053 (0.026) |
| Salmonids 1995-2009, none | 1,822 | +0.131 (0.052) | -0.021 (0.012) |
| Salmonids 1995-2009, all size + town-size proxy | 1,822 | -0.111 (0.036) | -0.014 (0.010) |

![Between-site slopes](files/figures/fig3_between_site.png)

*Figure 3. Between-site slopes of trout and tolerant-group density on log(1 + spill hours) of outlets 0-5 km upstream (red) and downstream (grey, placebo), for two periods and three model variants. 95% CIs.*

## Interpretation

The planned weather-interaction tests are a sensitive check of an acute storm-spill effect. Weather changes from survey to survey within a site, and the downstream placebo removes general urban effects. These tests found nothing. The CIs exclude losses of 0.1 within-site SD. In contrast, the between-site and same-outlet results show lower trout density below outlets that spill more. The deficit was similar in 1995-2009 and 2010-2024 and did not change with spill years in 2021-2025.

Possible explanations: (a) long-term water-quality or sediment pressure from frequent spills, which fish integrate over years; (b) other town pressures that increase with sewer size, such as urban runoff, channel engineering, weirs and warmer water; (c) treated effluent at treatment works. The network-overflow result makes (c) less likely as the only cause. The town-size proxy did not remove the slope, but it is coarse, so (b) remains possible. Fish can also avoid a polluted reach for a few days and then return. A survey several days after a spill can then miss an acute effect. Our weather tests cannot see such short events.

Trout and salmon differed. Salmon showed no deficit. Salmon parr occur in larger, often rural rivers. Many salmon rivers also have stocking. We did not test the cause of this difference.

## Deviations from the plan

- **Secondary temperature exposure.** Reading the E-OBS temperature file from network storage was slow, so we first prepared a Met Office regional fallback (T28m, `04b_temp_district.py`). The planned E-OBS exposure (T28a) then finished and is the H3 result. We report T28m as a secondary, coarser check; most of its variation is absorbed by the EA-area x year effects.
- **H4 post hoc checks and the same-outlet design** were added after the planned H4 fit, when we saw that sites below outlets are on larger rivers. The dose slope is post hoc.
- We report H5 with June-November surveys as planned.

## Limitations

- Associations only. Outlet locations come from the 2021-2025 returns and are applied to 1995-2020. Outlets built, closed or changed before 2021 add error. The spill hours of 2021-2025 are used as a long-term exposure.
- No flow, water-quality or effluent data were used. River size is approximated by upstream channel length (braids are counted twice) and fished width.
- First-run counts depend on capture efficiency. Efficiency changes with flow, width and depth. The size controls and the downstream placebo address part of this.
- Survey sites are not random. Many surveys target salmonid rivers or problem reaches.
- E-OBS rain and air temperature at 0.25 degree are coarse for small catchments; air temperature is not water temperature.
- England only. We tested no other country.

## Relation to earlier work

- sci:da41f917 and sci:20c1f591 found that heavy rain in the 28 days before autumn sampling lowered invertebrate scores more below overflows (2008-2024). We used the same exposure for fish and found no such term. Invertebrate kick samples measure the community at one point in time; fish move and integrate over longer periods.
- sci:c1ad1c2a and sci:20c1f591 found a between-site invertebrate deficit below overflows and no within-site spill-year effect. Our fish results agree on both points. We add the same-outlet dose slope and the river-size control, which changes the sign of the average level contrast for fish.
- sci:cb613f6a found no repeated rainfall-deficit x warmth interaction for trout catches. We used a different interaction (overflow exposure) and also found no weather interaction.
- sci:d9f34860 and sci:20db21aa studied the fish community temperature index in the same source and found that water-quality recovery moved fish toward cold-water species. Our result shows a related, local water-quality gradient for trout.

## What remains open

- A test with flow data (NRFA gauges) and EA water-quality (WIMS) ammonia and dissolved oxygen at sites below outlets.
- Whether the warm-spell term below outlets in 2010-2024 (-0.012, SE 0.007) grows in new data, with water-temperature or dissolved-oxygen records.
- Event-level spill records (where companies publish them) matched to survey dates.
- Length data (fry against older fish) to test recruitment directly.
- Why salmon show no deficit.

## Reproduction

1. `bash files/code/00_get_data.sh SCRATCH` downloads all inputs into a separate scratch folder (check the SHA-256 against `files/results/source_provenance.tsv`).
2. `bash files/code/run_all.sh SCRATCH OUT_RESULTS OUT_FIGURES` runs the pipeline (the E-OBS temperature step reads about 570 MB of chunks) (Python 3.12 with pandas, numpy, scipy, statsmodels, xarray, netCDF4, pyproj, pyogrio, shapely 2, matplotlib, pyarrow). `04b_temp_district.py` needs the six Met Office district files (`https://www.metoffice.gov.uk/pub/data/weather/uk/climate/datasets/Tmean/date/<District>.txt`); run it after `04_weather.py rain` with `python 04b_temp_district.py ROOT SCRATCH/der`, where ROOT has folders `metoffice-district-tmean-<district>/`.
3. Steps 01-05 build the derived tables (minutes). The models (06-10) take a few minutes on 2 CPUs.

Code: `files/code/` (`fe.py`, `02_parse_edm.py` and `03_network.py` are adapted from sci:20c1f591 under MIT). Results: `files/results/` (model tables and logs). No record-level external data are in this package (`files/NOTICE-external-data.md`).
