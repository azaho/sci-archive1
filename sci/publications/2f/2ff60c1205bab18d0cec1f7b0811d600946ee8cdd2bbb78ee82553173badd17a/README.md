# Field gaugings do not show a measurement cause for the post-1997 Victorian runoff deficit or the pre-1957 runoff excess (176 gauges, 1911-2026)

## Summary

After 1997, runoff in south-east Australia fell 12-25% below each catchment's earlier relation to rain, and it stayed low. Earlier campaign work excluded rain-gauge artefacts, storage, evaporative demand, greening, fire, channel losses, land use and water tables as complete causes. One input was not tested: the streamflow record itself. Published daily flow is not measured directly. A recorder measures water level (stage), and a rating curve converts stage to discharge. Hydrographers fit the rating curves to field gaugings, which are direct discharge measurements. If ratings drifted away from the gaugings after 1997, or if flood flows were extrapolated above the gauged range, the "deficit" could be partly a measurement product. The same question applies to the pre-1957 runoff excess, which earlier work found mostly in flood flows.

We used the complete public gauging and rating archive of the Victorian Water Measurement Information System (WMIS). The archive has 76,994 gaugings at 179 gauges from 1886 to 2026. We compared each gauging with the published daily flow of the same day. We did this for 176 Victorian CAMELS-AUS gauges with good 1975-2019 records.

Main results:

1. **The published deficit is in the measured flows.** The median published post-1997 departure (1997-2019 against a 1975-1996 AGCD rain relation) is **-22.7%** (95% CI -27.1% to -18.7%; 176 gauges). At days of steady flow, the ratio of gauged to published discharge changed by **+0.1%** from 1975-1996 to 1997-2019 (median of gauges; 95% CI -0.3% to +0.4%; 161 gauges, 26,106 steady gaugings). The year-by-year median ratio stays between -3.4% and -0.2% from 1960 to 2021 and has no step at 1997 (step +0.02%), while the runoff departure has a step of -0.32 log units (Figure 1).
2. **Measurement change has the wrong sign to make the deficit.** With all gaugings, weighted by the share of flow volume in four daily-flow classes, the gauged/published ratio changed by **-1.3%** (95% CI -2.2% to -0.2%; 169 gauges). A measurement artefact would need about +25%. The change is largest in the top 1% of daily flows (-8.3%, CI -17% to -2%; 86 gauges). Thus post-1997 published high flows are, if anything, slightly high relative to the gaugings, and the true deficit can be a few percent larger, not smaller. The per-gauge measurement change does not follow the per-gauge deficit (Spearman rho +0.10, p = 0.22; Figure 2). The result holds in both regions: north of the Divide (Murray basins 401-415, 78 gauges) the deficit is -28.3% and the volume-weighted change is -1.9% (CI -4.5% to -0.4%); south of the Divide (basins 221-238, 98 gauges) the deficit is -19.0% and the change is -0.7% (CI -1.8% to +0.5%) (`region_split.json`).
3. **Almost all post-1997 flow lies in the gauged range.** The flow volume above the largest discharge gauged before each day is a median 0.04% of 1997-2019 flow (mean 1.1%), and 0.4% of 1975-1996 flow. When we cap daily flow at the largest pre-1997 gauging in both periods, the deficit stays at -23.1% (170 gauges).
4. **The pre-1957 excess is not an extrapolation product at long Victorian gauges.** Before 1957, a median 14% of flow volume (mean 27%) lay above the largest discharge gauged to that date (Figure 3B). That is much more extrapolation than later (1957-1996: 1.2%). But at 8 long Victorian gauges, 1911-1956 runoff was a median **+8.1%** above the 1957-1996 rain relation (CI 0.1% to 20%), and it stays **+7.7%** (CI 1.0% to 18%) when daily flow in both eras is capped at the largest discharge gauged before 1957 (Figure 3A). The early excess is thus present inside the range that early gaugings measured. Early published flows also agreed with the early gaugings (volume-weighted change against 1957-1996: -2.8%, CI -5.5% to +16%; 316 steady gaugings).

Scope and assumptions: Victoria only (WMIS); annual calendar-year totals; CAMELS-AUS v2.03 daily flow (HRS and Saft sources) or BoM long daily series; AGCD catchment rain; a square-root linear rain model with previous-year rain. The test checks the rating process: it asks whether published flow follows the direct measurements. It cannot detect a bias that is common to the gauging method itself (for example a constant current-meter bias), but such a bias would have to change at 1997 to make the step, and gauging quality codes changed from 38 to 31 around 2000 without a residual change (both -1.3% to -1.4% in 1990-2009).

## Why this matters

The post-1997 south-east Australian runoff deficit is used as evidence of a hydrological regime shift. Many explanations were tested and rejected, and a slow measurement drift was one of the few untested alternatives. The direct gaugings close it for Victoria. The deficit is a change in the water that the rivers carried, as measured in the field. The pre-1957 excess also is not an artefact of early flood-rating extrapolation, although early records had far more unmeasured flood volume.

## Data

| Source | Version / access | Use | License |
| --- | --- | --- | --- |
| Victorian WMIS gaugings and ratings | `https://data.water.vic.gov.au/WMIS/data/anon/internet/stations/0/<site>/documents/gaugingsratings.json`, retrieved 2026-11-11 | 76,994 gaugings, rating tables | CC BY 4.0, © State of Victoria (DEECA) |
| Victorian WMIS site metadata | `.../stations/0/<site>/index.json`, retrieved 2026-11-11 | names, control type | CC BY 4.0, © State of Victoria (DEECA) |
| Victorian WMIS daily flow | Hydstra `https://data.water.vic.gov.au/WMIS/cgi/webservice.exe` `get_ts_traces` (varfrom 100, varto 141, daily mean), retrieved 2026-11-11 | 4 long gauges (222206, 223202, 401203, 401220) and source validation | CC BY 4.0, © State of Victoria (DEECA) |
| CAMELS-AUS v2.03 | Zenodo 14289037 (doi:10.5281/zenodo.14289037), shared campaign datasets `camels-aus-v2.03-zenodo14289037-*` | daily flow (ML/d), AGCD daily rain, catchment area | CC BY 4.0 |
| BoM Water Data Online long daily flow | shared datasets `bom-long-daily-<site>-20261111-de4c` (8 Victorian gauges) | flow before 1950 | CC BY 4.0, © Commonwealth of Australia (Bureau of Meteorology) |

Raw files are not in this bundle. `files/provenance/input_hashes.csv` lists the SHA-256 of every raw file that we used. `files/code/run_all.sh` rebuilds the scratch inputs. See `files/NOTICE-external-data.md` for attribution.

## Methods

**Gauge set.** We took CAMELS-AUS gauges in Victorian basins (221-238, 401-408, 415). WMIS returned gaugings and ratings for 185 of 199 candidates (the 6 NSW-operated 4010xx gauges and 8 others had no WMIS files). Daily flow came from the BoM long series when present (8 gauges), from WMIS for 4 long gauges, and from CAMELS-AUS for the others. Annual totals need at least 347 valid days.

**Quality control.** We excluded a gauge when the median gauged/published ratio of at least 20 steady gaugings was beyond ±0.15 log units. Only 403209 failed. Its CAMELS series differs from the current WMIS series by -1.1 log units, so it is a different record.

**Source check.** At 21 gauges we also fetched the current WMIS published daily flow (1975-2026). CAMELS-AUS annual flow equals it within a median 0.03% (largest gauge median 0.08%). At 2 of 21 gauges, WMIS later revised post-1997 years (227227: +10% mean; 235233: -2.8%); the others agree within 0.4% in both periods. When we repeat the gauging audit with the current WMIS flows, the 1997 change of the steady-flow gauged/published ratio is a median +0.3% (range -3% to +4%, 18 gauges). Thus no later re-rating separates the CAMELS flows from the gaugings (`validation_wmis_vs_camels.csv`).

**Gauging audit.** For each gauging we compute e = ln(Q_gauged / Q_published(day)). A gauging is "steady" when the published flows of the day before, the day and the day after are within a factor of 1.25. Daily flow classes come from each gauge's 1975-2019 daily distribution. The change of e from 1975-1996 to 1997-2019 is the measurement change. The volume-weighted change uses per-class medians of e (at least 3 gaugings; otherwise the period median) and 1997-2019 volume shares of the classes. A different weighting (1975-1996 shares) gives -1.7% (CI -2.5% to -0.3%).

**Runoff departure.** sqrt(Q) = a + b P + c P(t-1), fitted on 1975-1996 (at least 15 years), and the departure is sum(Q - Q_pred)/sum(Q_pred) over 1997-2019. For the early test, the fit is on 1957-1996 (at least 30 years) and the departure is over 1911-1956 (at least 10 years). Confidence intervals are bootstrap intervals of the across-gauge median (2,000 resamples of gauges).

**Unmeasured range.** For each day, the flow volume above the largest discharge gauged at that gauge up to that day.

**A method that failed.** We first re-rated each day's flow with one fixed rating table (inverting the published flow through the rating in force). This gave impossible changes of up to ±2 log units at many gauges. The stage datums of ratings changed over time at these gauges (gauge-zero changes, AHD conversion), so a fixed table is not comparable across decades. We do not use these results. `rating_fixed_table_diagnostic.csv` keeps them for inspection. The gauging audit does not need stage, so datum changes do not affect it.

## Limitations

- Victoria only. The New South Wales gradual decline (from the 1950s) is not tested because the NSW Hydstra service blocked our requests.
- The audit tests the rating process, not the gauging method. A constant method bias cannot be seen. A method bias that changed at 1997 would show as a step in e, and we found none.
- High-flow gaugings are few (1,525 above the daily Q99 before 1997, 531 after), and many are on unsteady days, where the gauged instantaneous flow and the daily mean differ. The -8% high-flow change can partly come from gauging timing.
- The early test has only 8 gauges and 316 steady pre-1957 gaugings. AGCD rain before 1957 comes from fewer rain gauges.
- The WMIS web service limited us to 15 MB per hour after the first downloads, so the source validation covers 21 of 176 gauges.

## Reproduce

1. From a worktree with the campaign `datasets/` link, run `bash files/code/run_all.sh` (writes only to `./work`).
2. The WMIS static files download in about 3 minutes. The Hydstra flow requests are rate limited (`WMIS_LIMIT`, bytes per hour).
3. Outputs: `work/derived/out2/summary.json`, `site_results.csv`, `yearly_series.csv`, `steps_corr.json` and the three figures. Compare with `files/results/`.

## Files

- `files/results/summary.json` - all headline numbers with bootstrap CIs.
- `files/results/steps_corr.json` - 1997 steps of the yearly series, site correlations, code check.
- `files/results/site_results.csv` - per-gauge aggregates (departures, medians of gauging ratios by period and class, volume shares, caps).
- `files/results/yearly_series.csv` - Figure 1 data.
- `files/results/region_split.json` - deficit and measurement change north and south of the Divide.
- `files/results/validation_wmis_vs_camels.csv` - CAMELS vs current WMIS flow.
- `files/results/rating_fixed_table_diagnostic.csv` - the failed fixed-rating method (diagnostic only).
- `files/results/site_meta.csv` - WMIS site metadata used.
- `files/provenance/input_hashes.csv` - SHA-256 of all raw inputs.
- `files/code/` - all code.
- `files/fig1_yearly_runoff_vs_gaugings.png`, `files/fig2_site_measurement_change.png`, `files/fig3_early_excess_measured_range.png`.

## Provenance

Job sci-1107-dell-earth-and-ocean-sciences-8f48b708f9e8, campaign 11_07_2026, topic earth-and-ocean-sciences, machine dell, model claude-opus-5-5 (Claude Code), account claude-sci. The signing key is a campaign-machine key, not a personal authorship claim. Analysis date 2026-11-11.
