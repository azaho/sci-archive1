# A reported solar-wind density link to next-day M5.6+ earthquake counts depends on one day (2011-03-11) and did not repeat in 2017-2026

## Summary

Marchitelli et al. (2020, Scientific Reports, doi:10.1038/s41598-020-67860-3) reported that the global rate of M5.6+ earthquakes increases on the first day after the daily mean solar-wind proton density falls below a threshold. Their best threshold was 15.5 protons per cm3 (band 12.7-15.9). They used SOHO CELIAS/MTOF Proton Monitor (PM) data and the ISC-GEM catalogue for 1996-2016. They gave a chance probability below 1e-5.

We did three tests:

1. **Replication (1996-2016).** We used the same SOHO data, the same statistic and the same null model. With ComCat (8,315 events) and with ISC-GEM magnitudes (7,459 events), we got the reported effect: R = 1.96 and R = 1.97, with p < 1e-5 under the paper's interval-shuffle null.
2. **Diagnosis.** One day causes all of the effect: 2011-03-11, the day of the Mw 9.1 Tohoku earthquake. That day has 105 ComCat (92 ISC-GEM) M5.6+ events. It is a "first day below threshold" only because the SOHO daily mean on 2011-03-10 was 17.98 cm-3. When we remove this single day, R = 1.03 (ComCat) and 1.06 (ISC-GEM), with p = 0.40 and 0.29. If we count days with at least one event (not events), R = 1.00. The OMNI (Wind/ACE) density for the same solar wind and the same 21 years gives R = 0.89, because OMNI had 10.3 cm-3 on 2011-03-10.
3. **Out-of-sample test (2017-01-01 to 2026-11-07).** We kept the specification fixed. OMNI at 15.5 cm-3 gave R = 1.13 (95% CI 0.85-1.52, p = 0.19; 90 condition days, 3,519 events). SOHO with a quantile-matched threshold gave R = 1.25 (0.84-1.77, p = 0.10). SOHO with the paper's min-max scaling gave R = 0.94 (0.82-1.08, p = 0.77). Declustered counts gave R = 1.01 (OMNI). No variant was significant. All upper confidence limits are below the in-sample R of 1.96.

We also found that the SOHO PM density scale changed relative to OMNI after 2015. The median SOHO/OMNI ratio was 1.00-1.23 in 1996-2015 and 0.76-0.91 in 2017-2026. Because of this, the SOHO series reached 15.5 cm-3 on only 4 days in 2017-2026, against 103 days for OMNI. A fixed SOHO threshold therefore cannot test the claim after 2016.

**Conclusion.** The data do not support a general effect of solar-wind proton density on next-day global earthquake rates. The published significance comes from one aftershock-rich day and from a null model that does not keep same-day clustering. A smaller effect (R about 1.2-1.4) cannot be excluded with the available data. This is the R size that we found in 1996-2005 SOHO data, and the out-of-sample confidence intervals include it.

## Question

Does the global M5.6+ earthquake rate increase on the first day after the daily mean solar-wind proton density falls below about 15.5 cm-3? Does this effect stay when (a) we use a different spacecraft, (b) we make the result independent of single aftershock days, and (c) we test new data from after the original study (2017-2026)?

## Data

| Data | Source / version | Use |
| --- | --- | --- |
| SOHO CELIAS/MTOF Proton Monitor hourly averages, 1996-01-20 to 2026-11-06 | https://space.umd.edu/pm/crn/ (Carrington rotations 1905-2317, retrieved 2026-11-08) | Daily mean proton density (hours with speed > 0 and Np > 0). This is the instrument of the original paper. |
| OMNI2 hourly (Wind/ACE, propagated to the bow shock), 1995-2026 | https://spdf.gsfc.nasa.gov/pub/data/omni/low_res_omni/ (retrieved 2026-11-08) | Independent daily mean proton density (word 24, fill 999.9 removed). |
| USGS ComCat, all M>=5.6 earthquakes 1996-01-01 to 2026-11-07 | FDSN event service, preferred magnitudes (89% Mw types), retrieved 2026-11-08 | Daily counts for the replication and out-of-sample test. |
| ISC-GEM catalogue as served by ComCat (`catalog=iscgem`), M>=5.6, 1996-2016 | FDSN event service, retrieved 2026-11-09 | Replication with the catalogue type of the original paper. All magnitudes are Mw. |

Daily values use UTC days. SHA-256 hashes of all 443 raw files are in `files/provenance/raw_file_sha256.txt`. The bundle has the derived daily table (`files/data/daily.csv`), the parsed SOHO hourly series (`files/data/soho_pm_hourly_1996_2026.csv.gz`), the ComCat event list (`files/data/events_M5.6.csv`) and the ISC-GEM event list. No campaign shared dataset was used. The shared store had no solar-wind or global catalogue data. We did not add the raw files to the shared store. `files/code/fetch_data.sh` downloads them again.

Note on the catalogue: the original study used ISC-GEM version 7.0 with 6,612 M5.6+ events. The direct ISC-GEM download needs a form with a CAPTCHA. We therefore used the ISC-GEM contributor catalogue that ComCat serves (7,459 events in 1996-2016, a later version) and ComCat preferred magnitudes (8,315 events). Both catalogues gave the same result.

## Method

- **Statistic (from the paper).** Condition day d: daily density on day d-1 >= T and daily density on day d < T (the paper's "first day below threshold", 1Dy bT). R = mean M5.6+ count on condition days / mean count on all other days with density data.
- **Specification.** We fixed the specification before the out-of-sample test: T = 15.5 cm-3, M>=5.6, the 1Dy bT condition, no declustering. We also report the mean R over the paper's band 12.7-15.9 (9 thresholds).
- **Threshold transfer after 2016.** We used three methods: (1) OMNI at the physical threshold; (2) SOHO quantile-matched (the same fraction of days above T as SOHO 15.5 in 1996-2016, 1.56%, which gives T = 11.24 cm-3 in 2017-2026); (3) SOHO with the paper's min-max scaling (V_step 0.38, which gives T = 6.94 cm-3). SOHO at the fixed 15.5 gives only 4 condition days, and we report it only for completeness.
- **Null models.** (a) The paper's null: synthetic catalogues from randomly permuted inter-event intervals (100,000 for the headline cases, 10,000-20,000 for the other cases). (b) A circular-shift null: we move the daily density series against the daily count series by every offset from 30 days to N-30 days. This keeps the autocorrelation and clustering of both series. p = (number of null R >= observed R + 1) / (number of null values + 1), one-sided.
- **Uncertainty.** 95% percentile bootstrap: we resample the condition days with replacement and the other days in circular 30-day blocks (4,000 replicates).
- **Robustness.** Days with at least one event (binary counts). Gardner-Knopoff (1974) declustering. Removal of the largest condition day. Magnitude thresholds 6.0, 6.5 and 7.0. Shallow (<60 km) and deep events. The paper's split into 1996-2005 and 2006-2016. Lags from -10 to +10 days. A threshold scan from 8 to 22 cm-3.

## Results

### 1. The in-sample effect replicates, but one day causes it

| Case (T = 15.5, M5.6+) | Condition days | R | 95% CI | p (paper null) | p (circular) |
| --- | --- | --- | --- | --- | --- |
| SOHO + ComCat, 1996-2016 | 103 | 1.96 | 0.83-4.09 | <1e-5 | 0.007 |
| SOHO + ISC-GEM, 1996-2016 | 103 | 1.97 | - | <1e-5 | 0.006 |
| SOHO + ComCat, 2011-03-11 removed | 102 | 1.03 | 0.77-1.35 | 0.40 | 0.39 |
| SOHO + ISC-GEM, 2011-03-11 removed | 102 | 1.06 | - | 0.29 | 0.30 |
| SOHO + ComCat, days with any event | 103 | 1.00 | 0.85-1.15 | - | 0.52 |
| SOHO + ComCat, declustered (GK) | 103 | 1.23 | 0.82-1.82 | - | 0.056 |
| OMNI + ComCat, 1996-2016 | 188 | 0.89 | 0.72-1.10 | 0.91 | 0.84 |
| OMNI + ISC-GEM, 1996-2016 | 188 | 0.90 | - | 0.88 | 0.81 |

The 103 SOHO condition days contain 218 events. The expected number is 111. The single day 2011-03-11 contributes 105 events (Figure 2A). After we remove it, the remaining 102 days have 113 events, which is the expected rate (Figure 2B). Figure 1 (top left) shows that the SOHO excess exists only for thresholds from about 9.7 to 17.9 cm-3. This is exactly the range for which 2011-03-11 is a condition day, because the SOHO daily means were 17.98 on 2011-03-10 and 9.62 on 2011-03-11. The hourly SOHO record shows a short density spike to 46 cm-3 (06-08 UT on 2011-03-10). OMNI recorded at most 20.8 cm-3 in its hourly values, and its daily mean was 10.3. In our replication, the larger R at M6.0+ (2.04) also depends on that day: 36 of the 2,797 ISC-GEM M6+ events in 1996-2016 occurred on 2011-03-11, and without that day R = 1.08 (circular p = 0.32). At M6.5+ the ISC-GEM R without that day is 1.36 (circular p = 0.14).

The paper's interval-shuffle null is too narrow (Figure 2C). Its standard deviation of R is 0.108, against 0.171 for the circular-shift null on the same data. The shuffle spreads each aftershock cluster over many days. So a synthetic catalogue almost never puts about 100 events on one day of 103, and an alignment of one condition day with one great earthquake looks like p < 1e-5. The circular-shift null keeps the cluster intact. It gives p = 0.007, which is the probability that one of 103 condition days falls on the Tohoku day (a small second mode near R = 2 in Figure 2C). With 4 solar variables, 5 conditions and many thresholds scanned in the original study, a coincidence of this size is not unexpected.

### 2. The paper's split samples

In 1996-2005 (the paper's "learning" set, before Tohoku), SOHO gives a moderate excess: R = 1.24 with ComCat (p_circ = 0.061) and R = 1.36 with ISC-GEM (p_circ = 0.032, p_shuffle = 0.010). The days-with-any-event version gives R = 1.08 (p = 0.20). OMNI gives R = 1.08 (ComCat) and 1.11 (ISC-GEM), both with p > 0.16. In 2006-2016 (the "testing" set), SOHO gives R = 3.63 with Tohoku and R = 0.60 (0.37-0.84) without it. OMNI gives R = 0.66. Thus the paper's statement that the learning-set parameters were confirmed in the testing set depends on the same single day.

### 3. Out-of-sample test, 2017-01-01 to 2026-11-07

| Density series and threshold | Condition days | R (M5.6+) | 95% CI | p (circular) | p (paper null) |
| --- | --- | --- | --- | --- | --- |
| OMNI, T = 15.5 | 90 | 1.13 | 0.85-1.52 | 0.19 | 0.15 |
| OMNI, T = 15.5, declustered (GK) | 90 | 1.01 | 0.76-1.26 | 0.49 | - |
| OMNI, T = 15.5, days with any event | 90 | 1.11 | 0.93-1.29 | 0.13 | - |
| OMNI, T = 15.5, M6.0+ / M6.5+ / M7.0+ | 90 | 0.88 / 1.32 / 0.91 | - | 0.73 / 0.21 / 0.63 | - |
| SOHO, quantile-matched T = 11.24 | 54 | 1.25 | 0.84-1.77 | 0.098 | 0.061 |
| SOHO, min-max scaled T = 6.94 | 378 | 0.94 | 0.82-1.08 | 0.77 | - |
| SOHO, fixed T = 15.5 | 4 | 1.02 | - | 0.49 | 0.51 |

No out-of-sample variant reaches p < 0.05. The band-mean statistic gives the same result (OMNI 1.08, p = 0.23). The largest OMNI condition day (2023-12-02, 12 events, Mindanao M7.6 sequence) gives most of the small positive R. Without it, R = 1.00. The lag profile (Figure 4) has no peak at lag +1 in OMNI in either period. The upper 95% limits (1.52 OMNI, 1.77 SOHO quantile-matched) exclude the in-sample R of 1.96. They do not exclude R of about 1.2-1.4.

### 4. SOHO PM density calibration changes with time

The SOHO/OMNI ratio of daily density is not constant (Figure 3, `files/results/soho_omni_calibration_by_year.csv`). It is 1.01-1.23 in 1996-2015 and 0.76-0.91 in 2017-2026. The year-to-year daily correlation is 0.66-0.94 (lowest in 2011). The yearly SOHO 98th percentile fell from 11-17 cm-3 to 9-12 cm-3, but the OMNI value stayed at about 14-20 cm-3. Studies that use one fixed SOHO PM density threshold across several decades will therefore select different solar-wind conditions in different years.

## Figures

- `files/figures/fig5_summary_forest.png`: R with 95% bootstrap CI for the main cases.
- `files/figures/fig2_one_day_and_nulls.png`: (A) events on each SOHO condition day; (B) R after we remove the largest days; (C) the paper's null and the circular-shift null.
- `files/figures/fig1_threshold_scan.png`: R against threshold for SOHO and OMNI, in sample and out of sample, with the 95% circular-shift null band.
- `files/figures/fig3_soho_omni_calibration.png`: SOHO/OMNI density ratio and days above 15.5 cm-3 per year.
- `files/figures/fig4_lag_profile.png`: R against lag from the last day above 15.5 cm-3.

## Limitations

- We did not use ISC-GEM version 7.0 itself. We used a later ISC-GEM version through ComCat and also ComCat preferred magnitudes. Event counts differ (6,612 vs 7,459 vs 8,315), but the replication values agree (R = 1.96-1.97). We did not verify that 2011-03-11 is a condition day in the authors' exact daily SOHO series. The SOHO PM archive can be reprocessed. Our series has a daily mean of 17.98 cm-3 on 2011-03-10.
- The paper gives its peak R values only in figures. Thus we compare with our own in-sample replication (R = 1.96), not with their exact numbers.
- We tested only density with the 1Dy bT condition, which the paper selected as its main result. We did not test proton flux (density x speed), which the paper also reported as significant.
- The out-of-sample data cover 9.85 years with 90 OMNI condition days. The test can reject R of about 1.96 but not R of about 1.2-1.4.
- OMNI densities are propagated to the bow shock and combine Wind and ACE. SOHO is at L1. Daily means of the two can differ for short structures, as on 2011-03-10.
- Bootstrap CIs treat condition days as independent. Thresholds were not corrected for the many variants that we report. All variants are in `files/results/relative_rates.csv` (176 rows).
- Gardner-Knopoff declustering uses fixed windows and is a coarse method.

## Reproduce

From an empty work directory with Python 3.12 (numpy, pandas, matplotlib; versions in `files/provenance/software_versions.txt`):

```bash
bash files/code/fetch_data.sh                    # downloads ~115 MB into ./raw
mkdir -p code && cp files/code/*.py code/
python -I code/build_daily.py raw derived        # daily density + counts
python -I code/run_analysis.py derived results   # main tables (~25 min, single core)
python -I code/run_iscgem.py raw/iscgem/comcat_iscgem_M5.6_1996-2016.csv derived results
python -I code/make_figures.py derived results figures
```

To reuse the archived inputs and skip the download, copy `files/data/daily.csv` and `files/data/events_M5.6.csv` into `derived/` and run the last three commands. Random seeds are fixed (20261108 and 7). New downloads can differ slightly, because ComCat magnitudes change and the live archives get new data.

## Files

- `files/code/`: `sw_eq_lib.py` (statistic, nulls, declustering), `build_daily.py`, `run_analysis.py`, `run_iscgem.py`, `make_figures.py`, `fetch_data.sh`.
- `files/data/`: derived daily table, parsed SOHO hourly series, ComCat and ISC-GEM event lists.
- `files/results/`: `relative_rates.csv` (all variants), `null_comparison.csv`, `null_samples.npz`, `iscgem_in_sample.csv`, `threshold_scan.csv`, `iscgem_threshold_scan.csv`, `lag_profile.csv`, `soho_omni_calibration_by_year.csv`, `meta.json`, run log.
- `files/provenance/`: raw-file SHA-256 list, software versions.

## Provenance

Campaign 11_07_2026, job sci-1107-dell-earth-and-ocean-sciences-eeba02a302d3, topic earth-and-ocean-sciences, machine dell, account claude-andrii. An AI agent (Claude Opus 5.5, model ID claude-opus-5-5) did the analysis and wrote the text in the SCI campaign harness on 2026-11-08/09 UTC. The signing key is a campaign-machine key. It does not make a personal authorship claim.
