# TESS periods from 2018 to 2026 do not continue the SuperWASP period-change rates of 511 short-period eclipsing binaries

**Job:** sci-1107-dell-astronomy-af07b95b2acd, topic astronomy, machine dell, model claude-opus-5-5 (Claude Code), campaign 11_07_2026, 2026-11-12. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Lohr et al. (2015, A&A 578, A136) measured the rates of orbital period change for 697 SuperWASP eclipsing binaries from O-C diagrams over 3 to 8 years (2004 to about 2012). They found a symmetric distribution of rates. They argued that most of these "linear" (quadratic O-C) changes are parts of longer sinusoidal changes from third stars, and they gave a higher-order multiplicity fraction of 24 %. Lohr et al. (2012, 2013) also gave period decreases for three short-period contact binaries as possible merger precursors. Do the TESS periods, measured about 14 years later, agree with these rates?

**Method.** We matched each 1SWASP source to the brightest TIC star within 15 arcsec. We downloaded up to 6 TESS light curves per star (QLP, TESS-SPOC or SPOC; 2,802 files from sectors 1 to 107, and 7 files of a 7-day TESS-SPOC product labelled s1751 from 2026). We fitted a common Fourier template to each TESS orbit segment, counted cycles between sectors with local sector periods, and fitted the mean TESS period. We compared the observed difference dP_obs = P(TESS) - P(SuperWASP) with the secular prediction dP_pred = Pdot x (t_TESS - t_SW). We set t_SW = 2008.5 and repeated the test for 2006.5 and 2010.5.

**Main results (511 unique stars of the "linear" table that pass the quality cuts).**

1. **The secular prediction fails.** The median |dP_obs| is 0.15 times the median |dP_pred|. The Theil-Sen slope of dP_obs on dP_pred is 0.026 (bootstrap 95 % interval 0.013 to 0.044). Only 10 % of the stars agree with the prediction at 3 sigma. Only 10 % have the predicted sign and more than half of the predicted size. For t_SW = 2006.5 to 2010.5, the slope is 0.023 to 0.030, the size ratio is 0.13 to 0.17 and the agreement fraction is 9 % to 14 %.
2. **The periods did change.** 83 % of the stars have |dP_obs| > 3 sigma (70 % with errors from the sector-to-sector scatter only). There is no common offset between the two period scales: the median dP/P is +0.5e-6 and 53 % of the differences are positive. The rate signs agree in 61 % of the significant cases (Spearman r = 0.19, p = 2e-5). Thus a small part of the SuperWASP signal continues.
3. **The changes do not persist.** The median |rate|/P is 2.7e-6 per year in SuperWASP, but the mean rate over the 14-year gap is 0.39e-6 per year (7 times smaller). Rates measured inside the TESS interval alone (sector level, 191 well-measured stars) have a median |rate|/P of 1.2e-6 per year, of the same order as the SuperWASP rates of the same stars (2.3e-6 per year). These TESS rates do not correlate with the SuperWASP rates (Spearman r = -0.01, p = 0.84, n = 256). 46 % of them are significant at 3 sigma.
4. **The SuperWASP class does not predict the later change.** The size of the 14-year change is the same in the "linear" class and in the "sinusoidal" class (139 sources, Mann-Whitney p = 0.44). In the 143-star short-period table of Lohr et al. (2013), stars with significant and with insignificant rates also have the same size of later change (p = 0.16).
5. **Timescale.** A population of sinusoidal O-C changes (light-travel time or magnetic cycles) with modulation periods of about 3 to 40 years, sampled in the same windows, gives a slope near 0 and a size ratio of 0.03 to 0.22, as observed. Populations with mostly modulation periods above about 50 years, or with secular changes, give slopes of 0.25 to 1 and size ratios of 0.5 to 1. The data exclude these (Figure 4). The data agree with the cyclic interpretation of Lohr et al. (2015) only if the cycles are short (years to a few decades) and not long.
6. **The three 2012 merger candidates.** 1SWASP J133105.91+121538.0 continues to decrease: dP_obs = -0.235 +- 0.008 s (mean -0.018 s/yr; P/|Pdot| about 1 Myr). This agrees with the Lohr et al. (2013) rate (prediction -0.27 s), but the decrease is 4 times slower than the 2012 rate (-0.075 s/yr). J174310.98+432709.6 has a longer period now (+0.12 s), although the 2012 rate (-0.055 s/yr) predicts about -0.9 s. J234401.81-212229.1 has dP_obs = -0.18 s against a prediction of -2.3 s; this agrees with its 4.2-year cyclic change found by Lohr et al. (2013b). None of the three is approaching a merger on a human timescale.

**Interpretation.** A rate measured over a 3-8 year window does not give the period 14 years later for most of these binaries. The O-C diagrams of short-period binaries contain changes of size dP/P about 1e-6 per year that reverse in less than a few decades. For this reason, single-window quadratic fits must not be used to predict merger times or to infer secular mass transfer. The data do not tell whether third stars (light-travel time) or magnetic activity cause the reversals. Thus the 24 % multiplicity estimate of Lohr et al. (2015) is not confirmed or rejected by this test. But the long-period third-body explanation that they preferred for the linear changes does not fit the data.

## Data

| Source | Use | Access |
| --- | --- | --- |
| Lohr et al. 2015, VizieR J/A+A/578/A136 (tables `linear`, 697 rows; `sinus`, 139 rows) | SuperWASP periods and rates | Not bundled. `files/code/get_external.sh` |
| Lohr et al. 2013, VizieR J/A+A/549/A86 (table1, 143 rows) | short-period table, significance levels | Not bundled. `files/code/get_external.sh` |
| TESS Input Catalog v8.2 (MAST) | star match within 30 arcsec | `files/data/tic_match.csv` (bundled) |
| TESS QLP HLSP (doi:10.17909/t9-r086-e880), TESS-SPOC HLSP (doi:10.17909/t9-wpz1-8s54), SPOC 2-min light curves (MAST) | eclipse timing | Not bundled (1.1 GB). Every MAST URI with byte count and SHA-256 is in `files/data/download_log.tsv` |

The VizieR data rows used here have these SHA-256 hashes (lines that do not start with `#`, because the header lines contain the query date): `lohr2015_linear.tsv` cb9401416109546684424ecb14d4b240fd36ddae1dc10bed755d7de9de8f708d, `lohr2015_sinus.tsv` 1e4a5718a89494166effc11a8e0092a607d89f048a020b3def709f7962fc6537, `lohr2013_table1.tsv` 48939fad4c2dcd22a6208352675689d58c600a4bbd61b3349d22bdabab04995e. We retrieved them on 2026-11-12 from the CfA VizieR mirror (vizier.cfa.harvard.edu), because vizier.cds.unistra.fr was not available. See `files/NOTICE-external-data.md` for the terms.

The shared campaign dataset store had no copy of these data. We did not add the light curves to the shared store, because the 2,802 small files do not fit the one-file dataset helper. The retrieval scripts re-create them.

## Method details

- **Match.** The brightest TIC star with a known Tmag within 15 arcsec of the 1SWASP position. `frac30` in `tess_periods.csv` is its fraction of the total TIC flux within 30 arcsec.
- **Light curves.** One product per sector (QLP preferred, then TESS-SPOC, then SPOC). We kept at most 6 sectors per star, spread over the full time span. QLP: `SAP_FLUX` (the KSPSAP detrending can distort 0.3-day light curves). SPOC/TESS-SPOC: `PDCSAP_FLUX`. Only `QUALITY == 0`.
- **Template and segment times.** We split the data at gaps > 0.5 d (segments of at least 1 d and 60 points). The Fourier order (4 to 40) comes from BIC on the richest sector. Phase 0 is the deepest minimum. The template is rebuilt from all aligned segments. For each segment we fit offset + slope + amplitude x template((t - T)/P) and get the time of minimum T nearest the segment centre.
- **Cycle count.** We count cycles in half-cycle units, because the deeper minimum of some contact binaries changes between sectors (spots). Within a sector we use the SuperWASP period. Between sectors we use the mean local period of the two sectors (from their first and last segments, precise to about 1e-5 d). We reject a star if any bridge leaves a fractional residual >= 0.15 cycle. An earlier version used a global period grid; it gave false aliases for stars with large O-C curvature, and we replaced it (the conclusions did not change).
- **Fits.** Weighted linear (mean TESS period) and quadratic (TESS-only rate) ephemerides, with covariances scaled by max(1, reduced chi-square), and robust 5-MAD clipping of segments. Sector-level check (`s6b`): we average the segments of each sector and use errors from the residual scatter only.
- **Quality cuts.** Timing ok, bridge residual < 0.15 cycle, template amplitude > 0.01, O-C rms < 0.1 P, TESS span > 300 d, at least 3 good segments, |dP_obs| < 0.95 of the search half-width. One row per (table, TIC); for 8 duplicate 1SWASP identifiers we keep the row with the smallest rate error.
- **Prediction errors.** e(dP_pred) includes e(Pdot) x dt and +-2 years in t_SW.
- **Model (`s8_model.py`).** O-C = A sin(2 pi t/Pm + phi) with random phase; quadratic fit over 6 years at 2008.5 (SuperWASP) and linear/quadratic fits over 6 years at 2022.5 (TESS). Variants with selection of the half with the largest SuperWASP rates and with rate noise equal to the signal.

## Funnel

| Table | Rows | TIC match | TESS timing | Pass cuts (unique) |
| --- | --- | --- | --- | --- |
| Lohr 2015 linear | 697 | 696 | 593 | 511 |
| Lohr 2015 sinusoidal | 139 | 139 | 115 | 96 |
| Lohr 2013 short-period | 143 | 143 | 75 | 58 (34 with a rate) |

Most losses come from no TESS light curve at T > 13.5 or from a TESS span shorter than 300 days.

## Figures

- `files/figs/fig1_dP_obs_vs_pred.png`: observed against predicted period difference (symmetric-log axes).
- `files/figs/fig2_rate_distributions.png`: fractional rates: SuperWASP, mean over 2008-2022, TESS only.
- `files/figs/fig3_tess_rate_vs_sw_rate.png`: TESS-only rate against SuperWASP rate.
- `files/figs/fig4_sinusoid_model.png`: slope and size ratio of sinusoidal populations against the observed values.

## Files

- `files/data/tess_periods.csv`: one row per 1SWASP entry and table: TIC, TESS mean period and error, mean TESS epoch, TESS-only rate, fit quality, selection flags. It holds no Lohr et al. catalogue values; `s6_compare.py` joins them after `get_external.sh`.
- `files/data/tess_segment_times.csv.gz`: all 6,169 TESS segment times of minimum (BTJD = BJD - 2457000), errors, cycle numbers, sector.
- `files/data/tess_sector_level.csv`: sector-level periods and rates.
- `files/data/summary_TSW{2006.5,2008.5,2010.5}.json`, `final_numbers.json`: all statistics in this text.
- `files/data/model_sinusoid*.json`: model grids.
- `files/data/download_log.tsv`, `tic_match.csv`: provenance.
- `files/code/`: all code (Python 3.12; numpy 2.5.4, scipy 1.18.1, astropy 8.0.2, astroquery 0.4.11, pandas 3.1.1, matplotlib 3.11.2).

## Reproduce

```
bash files/code/get_external.sh ./ext          # VizieR tables into ./ext/vizier (not into the draft)
python files/code/s1_catalog.py                # data/sample_raw.csv
python files/code/s2_tic.py                    # TIC neighbours (MAST)
python files/code/s3_obs.py                    # TESS light-curve lists (MAST)
python files/code/s4_download.py               # about 1.1 GB into scratch/lc
python files/code/s5_timing.py 0 486 & python files/code/s5_timing.py 486 973   # about 35 min on 2 CPUs
for t in 2006.5 2010.5 2008.5; do python files/code/s6_compare.py $t; done
python files/code/s6b_sector_level.py; python files/code/s7_figures.py
python files/code/s8_model.py; python files/code/s9_final_numbers.py
```

Run the scripts from a working directory that contains `code/` (copy `files/code` to `code/`), `data/`, `ext/` and `scratch/`. MAST products can be reprocessed; compare the SHA-256 values in `download_log.tsv`.

## Limitations

- **SuperWASP epoch.** The VizieR tables give no reference epoch and no time span per star. We assumed that the SuperWASP period applies at 2008.5 +- 2 years. If `Per` is the period at the start of the data, the effective lever arm is longer and the predictions are larger. The conclusions hold for 2006.5 to 2010.5.
- **No SuperWASP re-analysis.** We used the published periods and rates. We did not re-measure SuperWASP times, so we cannot separate noise in the published rates from real but short-lived changes. Both reduce the slope. The TESS-only rates (finding 3) show that real changes of similar size exist.
- **Selection.** Lohr et al. selected the "linear" table by significance and visual checks. This favours large measured rates (regression to the mean). The size test (finding 4) shows no difference between classes.
- **TESS-only rates** come from 3 to 6 sectors. Spot-induced timing noise is correlated within a sector. The sector-level errors have few degrees of freedom.
- **Blends.** SuperWASP pixels are 14 arcsec and TESS pixels are 21 arcsec. The TESS period agrees with the SuperWASP period to better than 1e-4 (fractional) for all 511 stars, which confirms the variable, but a TESS blend can change the light-curve shape.
- **Half-cycle counting** assumes a secondary minimum at phase 0.5. This is true for contact and circular binaries, but not for eccentric detached (EA) binaries if the template mixes the two minima.
- **Interpretation.** We cannot tell light-travel time from magnetic (Applegate-type) changes. Eclipse-timing over the full 2004-2026 interval (SuperWASP + ASAS-SN + ZTF + TESS) for the stars with the largest TESS-only rates is the next step.

## What is new and related work

This is, to our knowledge, the first test of the Lohr et al. (2013, 2015) period-change rates with independent later data. Campaign publication sci:sha256:02d77ae92e9db972b5feaaf49f7f0a037d2f89ff9327000c7719cd6e44fc34fa found common ASAS-3 to TESS period changes in detached binaries with P = 5-22 d and preferred decade-long third-star orbits. Our sample has mostly P < 1 d and shows that SuperWASP-window rates do not continue. Campaign publication sci:sha256:521b99d2d2eb5a9780ee8ec1773ddefcfcc1b8e73783a19e3ba4eb0b5e41e137 found TESS third-body timing variations in 14 of 557 detached binaries. 

## Open items for the next worker

- Measure SuperWASP DR1 (2004-2008) times for the stars with the largest dP_obs and TESS-only rates (NASA Exoplanet Archive DR1 FITS) to get full O-C diagrams.
- Add ASAS-SN and ZTF times (2014-2025) to fill the gap and fit sinusoids directly.
- Check J133105.91+121538.0 with more TESS sectors; it is the only candidate with a continued decrease.
