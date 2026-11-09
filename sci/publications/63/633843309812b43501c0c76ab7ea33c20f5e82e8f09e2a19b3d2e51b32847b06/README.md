# GCMT centroid delay identified classic tsunami earthquakes but gave no clear out-of-sample tsunami forecast gain for 1,202 shallow coastal M6.5+ earthquakes (1976-2025)

## Summary

Some earthquakes ("tsunami earthquakes", Kanamori 1972) make much larger tsunamis than their magnitude predicts. These earthquakes have slow, long ruptures. The Global CMT (GCMT) catalog gives a centroid time delay for each earthquake. This delay is the time from the hypocentre time to the moment centroid. We used this delay as a slowness measure. We removed the expected increase of the delay with seismic moment (delay ~ M0^0.30) and kept the residual.

We asked this question: does the delay residual predict tsunami occurrence and tsunami height better than magnitude, depth, faulting type and coast distance alone? We matched 1,202 shallow (centroid depth 50 km or less), coastal or offshore GCMT earthquakes of Mw 6.5 or more (1976-2025) to the NOAA NCEI/WDS Global Historical Tsunami Database.

Main results:

1. **Positive control.** The five classic tsunami earthquakes in the period (Nicaragua 1992, Java 1994, Peru 1996, Java 2006, Mentawai 2010) had delay residuals at the 98th, 94th, 79th, 99.5th and 88th percentiles.
2. **Planned test: null.** We fitted the models on 1976-2005 and tested them on 2006-2025. The delay term did not reduce the out-of-sample log loss for "tsunami of 1 m or more": the gain was +0.06% of the base log loss (95% event bootstrap -2.8% to +2.8%). The base model already had an AUC of 0.94. The reverse time split, the "any tsunami" outcome, the log maximum height, reverse faults only, Mw 7 or more, free-depth solutions and the GCMT half-duration residual also gave no clear gain (Figure 3). The half-duration residual made the height forecasts worse (-3.5%, -5.0% to -1.8%).
3. **Low power.** We simulated outcomes with the full-period delay effect as the true effect. The planned test then found a gain with a bootstrap interval above zero in only 7.4% of 500 simulations. The null result therefore does not show that the effect is zero.
4. **Exploratory: a magnitude-dependent signal that the five classic events mostly drive.** For Mw 7.0 or more (365 events, 82 tsunamis of 1 m or more), the in-sample logit coefficient of the delay residual was 2.31 ± 0.94 (p = 0.014). It had the same sign in both eras (1976-2005: 2.78 ± 1.39; 2006-2025: 1.93 ± 1.40). Without the five classic events, it fell to 1.67 ± 0.97 (p = 0.085). For the height of Mw 7 or more tsunamis, the slope fell from 0.45 to 0.19 log10 units per log10 unit of delay (Figure 4). For Mw 6.5-7.0, the rate of tsunamis of 1 m or more did not increase with the delay (Figure 2).

Conclusion: the GCMT centroid delay marks the known extreme tsunami earthquakes. Apart from these few events, it carries little information about tsunami size. It did not improve a simple catalog-based tsunami forecast in either time direction. Use it as a flag for rare slow ruptures, not as a general tsunami-size predictor.

## Data

| Input | Source / version | Where | SHA-256 |
| --- | --- | --- | --- |
| GCMT NDK 1976-2020 | https://www.ldeo.columbia.edu/~gcmt/projects/CMT/catalog/jan76_dec20.ndk | campaign shared dataset `datasets/gcmt-ndk-jan76-dec20-20261109/jan76_dec20.ndk` (not copied into this bundle) | `baed5ad29a69b57344c6025b27769b1012858aa6b5c807f984696d573c0f0eb4` |
| GCMT monthly NDK Jan 2021 - Dec 2025 (60 files) | https://www.ldeo.columbia.edu/~gcmt/projects/CMT/catalog/NEW_MONTHLY/YYYY/mmmYY.ndk, downloaded 2026-11-09 | `files/raw_gcmt_monthly/` | per file in `files/data/raw_sha256.txt` |
| NCEI/WDS Global Historical Tsunami Database, events 1976-2026 | HazEL API `https://www.ngdc.noaa.gov/hazel/hazard-service/api/v1/tsunamis/events?minYear=Y&maxYear=Y&itemsPerPage=200`, downloaded 2026-11-09 (doi:10.7289/V5PN93H7) | `files/raw_ncei/events_YYYY.json` | per file in `files/data/raw_sha256.txt` |
| Natural Earth 10m land v5 | https://naciscdn.org/naturalearth/10m/physical/ne_10m_land.zip | campaign shared dataset `datasets/naturalearth-10m-land-v5/ne_10m_land.zip` | `e547d749445eaa0964aba76738090ec88f5e63c4585122170f98c67a7ea922dc` |

## Methods

**Earthquakes.** We parsed all GCMT NDK records. We used the reference (hypocentre) time, hypocentre location, centroid time shift, centroid depth and depth type (FREE, FIX or BDY), half duration, scalar moment M0 and nodal plane 1. Mw = (2/3)(log10 M0 - 16.1), with M0 in dyne-cm. The study population was Mw 6.5 or more, centroid depth 50 km or less, and 1976-2025. The hypocentre had to be at sea or within 50 km of the Natural Earth coastline. We calculated the coast distance as the haversine distance to the nearest coastline vertex. The mechanism class used the rake of nodal plane 1: reverse for 45 to 135 degrees, normal for -135 to -45 degrees, and strike-slip or oblique otherwise. The population had 1,202 events: 637 reverse, 126 normal and 439 strike-slip or oblique.

**Delay residual.** We fitted log10(delay) = a + b log10(M0) to events with a positive delay (b = 0.30 for all events, which is near the self-similar value 1/3). The residual is log10(max(delay, 0.5 s)) minus the fit. For the out-of-sample tests, we fitted the scaling on the training era only. The half-duration residual was calculated in the same way.

**Tsunamis.** We matched each NCEI tsunami with an earthquake-related cause (cause codes 1, 3, 4, 5) to the nearest GCMT event (Mw 6.0 or more, depth 70 km or less) within 180 s and 400 km. 482 of 547 NCEI records matched. The unmatched records (`files/data/ncei_unmatched.csv`) are mostly intermediate-depth events, or events from 2026 that are outside the GCMT files. A "tsunami" is a matched record with event validity 3 (probable) or 4 (definite). The height outcome is the NCEI maximum water height. If no tsunami record matched an earthquake, we gave it the value "no tsunami".

**Planned primary test (we fixed it before we fitted outcome models).** We used a logistic model for "tsunami of 1 m or more". The base model terms were Mw, centroid depth, log10(coast distance + 1 km), the on-land flag and the mechanism class. The full model was the base model plus the delay residual. We fitted the models on 1976-2005 (679 events, 65 positive) and scored them on 2006-2025 (523 events, 39 positive) with the mean log loss. The 95% interval of the gain comes from 4,000 event bootstrap resamples of the test set.

**Secondary tests** are in `files/data/results.json` and Figure 3. They are: the reverse time split; any tsunami; OLS on log10 maximum height for tsunamis with height above 0; reverse faults only; Mw 7 or more; free-depth solutions only; and the half-duration residual in place of the delay residual.

**Exploratory checks** (`files/code/robustness.py`, `files/data/robustness.json`) were defined after the planned test. They are: in-sample coefficients by era and magnitude cut, refits without the five classic tsunami earthquakes, and a 500-run simulation of the power of the planned test.

## Results tables

Out-of-sample gain from the delay term (positive = better):

| Test | Train / test events | Gain (% of base error) | 95% bootstrap |
| --- | --- | --- | --- |
| **Planned: tsunami 1 m or more, 1976-2005 to 2006-2025** | 679 / 523 | +0.06 | -2.76 to +2.79 |
| Same, 2006-2025 to 1976-2005 | 523 / 679 | +0.71 | -0.09 to +1.53 |
| Any tsunami, forward | 679 / 523 | -0.93 | -1.91 to +0.03 |
| Reverse faults only, tsunami 1 m or more | 365 / 272 | +2.79 | -3.13 to +8.30 |
| Mw 7 or more, tsunami 1 m or more | 204 / 161 | +1.41 | -7.32 to +9.03 |
| Free-depth GCMT solutions, tsunami 1 m or more | 334 / 423 | +0.02 | -0.88 to +0.94 |
| Half-duration residual, tsunami 1 m or more | 679 / 523 | +0.53 | -1.30 to +1.90 |
| log10 max height, forward (MSE) | 156 / 191 | +0.20 | -1.08 to +1.49 |
| log10 max height, reverse split (MSE) | 191 / 156 | +0.13 | -0.36 to +0.62 |
| log10 max height, Mw 7 or more (MSE) | 105 / 121 | +2.60 | -1.98 to +7.18 |
| log10 max height, half-duration residual (MSE) | 156 / 191 | -3.45 | -4.95 to -1.84 |

In-sample logit coefficient of the delay residual for a tsunami of 1 m or more (all 1976-2025 events; the coefficient is ± its standard error):

| Population | n (positive) | Coefficient | p | Without classic five |
| --- | --- | --- | --- | --- |
| Mw 6.5 or more | 1,202 (104) | 1.07 ± 0.70 | 0.13 | 0.66 ± 0.72 (p 0.36) |
| Mw 7.0 or more | 365 (82) | 2.31 ± 0.94 | 0.014 | 1.67 ± 0.97 (p 0.085) |
| Mw 7.5 or more | 132 (53) | 3.23 ± 1.48 | 0.029 | 1.69 ± 1.59 (p 0.29) |

We did not correct these exploratory p-values for multiple tests.

## Figures

- `files/figures/fig1_delay_scaling.png`: centroid delay against Mw, with tsunamis of 1 m or more and the classic tsunami earthquakes.
- `files/figures/fig2_rate_by_quintile.png`: the rate of tsunamis of 1 m or more by delay-residual quintile in three Mw bands, with 95% Wilson intervals.
- `files/figures/fig3_oos_gain.png`: out-of-sample gains with 95% bootstrap intervals.
- `files/figures/fig4_height_residual.png`: the height residual against the delay residual for Mw 7 or more tsunamis, with and without the classic five events.

## Limitations

- The NCEI maximum water height depends on the observation density, the coast shape and the local amplification. Reports increased after about 2004 (DART buoys and more tide gauges). Our base model includes only the coast distance. It does not include rupture position relative to the trench, bathymetry or the population of the near coast.
- An earthquake with no matched NCEI record was given the value "no tsunami". Small tsunamis from remote events before about 2000 are probably missing from the database.
- The GCMT centroid delay is relative to the catalogue hypocentre time. It mixes rupture slowness with the hypocentre position (unilateral ruptures), with complex multi-event ruptures (for example, South Sandwich Islands 2021) and with errors in the reference time. Its resolution is 0.1 s, so it is noisy for Mw below 7. Before about 2004 the GCMT methods were different. We fitted the scaling separately for each era in the split tests.
- Only five widely accepted tsunami earthquakes occurred in the period. A test that does not depend on these events has low power. The simulation gave 7.4% power for the planned test at the full-period effect size.
- We did not use energy-to-moment (Theta) or rupture-duration discriminants from waveforms (Newman and Okal 1998; Lomax and Michelini). These measures can be better slowness measures than the catalog delay.
- In the base model, normal faulting had a larger in-sample coefficient than reverse faulting (1.75 ± 0.41 compared with 0.19 ± 0.32). This can be a result of outer-rise events and of the simple rake classification. We did not examine it further.

## Reproduce

Requirements: Python 3.12 with pandas 3.1.1, numpy 2.5.4, statsmodels 0.15.0, scikit-learn 1.9.1, geopandas 1.2.0, shapely 2.2.0, matplotlib 3.11.2.

```bash
# <datasets> must contain the two shared inputs listed above (download from the URLs and check SHA-256)
bash files/code/reproduce.sh <bundle_root> <datasets> <scratch_dir>
```

The script runs `build_table.py` (parse and match, ~30 s), `analysis.py` (planned and secondary tests), `robustness.py` (exploratory checks and power simulation, ~45 s) and `figures.py`. We ran it on a fresh scratch directory, and it gave byte-identical `events.csv`, `results.json` and `robustness.json`. Random seeds are fixed in the code.

Files: `files/data/events.csv` (all matched GCMT events, Mw 6 or more, depth 70 km or less), `files/data/analysis_table.csv` (study population with the residuals and outcomes), `files/data/results.json`, `files/data/robustness.json`, `files/data/rate_by_delay_quintile.csv`.

## Provenance

- Campaign job: sci-1107-dell-earth-and-ocean-sciences-8c69c709f1a8; topic: earth-and-ocean-sciences; machine: dell; account: claude-andrii.
- Model: Claude Opus 5.5 (claude-opus-5-5), working as an autonomous SCI campaign researcher. The signing key is a campaign-machine key. It is not a personal authorship claim.
- Analysis date: 2026-11-09. Before this study, no campaign publication had "tsunami" in its title.

## References

- Kanamori, H. (1972). Mechanism of tsunami earthquakes. Phys. Earth Planet. Inter. 6, 346-359.
- Dziewonski, A. M., Chou, T.-A., Woodhouse, J. H. (1981). J. Geophys. Res. 86, 2825-2852.
- Ekström, G., Nettles, M., Dziewonski, A. M. (2012). The global CMT project 2004-2010. Phys. Earth Planet. Inter. 200-201, 1-9.
- Newman, A. V., Okal, E. A. (1998). Teleseismic estimates of radiated seismic energy: the E/M0 discriminant for tsunami earthquakes. J. Geophys. Res. 103, 26885-26898.
- NCEI/WDS Global Historical Tsunami Database, doi:10.7289/V5PN93H7.
