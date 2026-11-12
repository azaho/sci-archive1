# Gaia XP H-alpha emission of 132 TESS CPV hosts is the same as that of matched young rapid rotators; a mean circumstellar excess above about 0.7 A is excluded

**Job:** sci-1107-dell-astronomy-94f7852c7266. **Campaign:** 11_07_2026. **Topic:** astronomy. **Machine:** dell. **Account:** claude-sci. **Model:** Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. **Date:** 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Complex periodic variables (CPVs) are young, rapidly rotating M dwarfs with sharp flux dips at the rotation period. The dips probably come from material near the corotation radius. Bouma et al. (2026, arXiv:2609.00136) found H-alpha emission from cool plasma clumps that corotate with two CPVs (TIC 141146667 and TIC 300651846). In TIC 300651846, the clump emission was about 60% of the stellar H-alpha equivalent width (EW about 3.6 A) on one night, about 10% (about 0.6 A) on other nights, and zero on one night. In a third CPV (LP 12-502) there was no clump emission (< 0.01 A). Thus it is not known if bound plasma is a general property of CPV hosts, and if hosts have more of it than other young rapid rotators.

We tested this at population level. We used the Gaia DR3 H-alpha pseudo-equivalent width from the RP spectrophotometry (ESP-ELS `ew_espels_halpha`) of the TESS CPV survey stars of `sci:sha256:22057485` and `sci:sha256:b46f8555`. Gaia averages these spectra over about 40-70 transits in 34 months. We compared 117 CPV hosts with 1,706 non-host rapid rotators in the same window (P 0.15-1 d, BP-RP 2.4-3.8), at a fixed colour, BANYAN age class, rotation period and height above the main sequence (dMG). We calibrated the Gaia scale with spectroscopic H-alpha EWs of 1,307 nearby M dwarfs (Newton et al. 2017).

Main results:

1. **The Gaia measurement is sensitive to chromospheric H-alpha.** In the calibration stars, the Gaia pseudo-EW changes by 0.039 +/- 0.005 nm per A of true EW in active stars (0.056 nm/A in all stars). Rapid rotators have 0.154 +/- 0.008 nm more emission than other red dwarfs of the same colour and class (about 4 A on the true scale).
2. **The apparent H-alpha excess of hosts comes from their youth.** With colour only, hosts emit 2.9 +/- 0.6 A more than non-host rapid rotators (p = 1e-10). With age class, the excess falls to 1.5 +/- 0.5 A. With age class, period and height, the host offset is +0.23 A (bootstrap 95% interval -0.70 to +1.16 A; positive = less emission). Inside the 1-200 Myr groups, the offset is -0.13 +/- 0.53 A even without the height term (Figure 1b).
3. **A mean circumstellar excess above about 0.7 A is excluded (95%).** This is about 12% of the median H-alpha EW of nearby M dwarfs with P < 1 d (5.7 A). Sixteen variants (members only, 15-24 Myr only, RUWE < 1.4, extra photometric terms, a robust fit, quantile fits, the observed-minus-synthetic pseudo-EW, an x-based model, splines, the S1-S55 replication sample and both samples together) give offsets from -0.39 to +0.84 A. No variant has a significant host excess.
4. **Matched controls agree.** Each host minus the mean of its 10 nearest non-hosts in the same age class (colour, period, height and G) gives +0.021 nm (-0.009 to +0.050 nm), about +0.5 A, with a permutation p = 0.38.
5. **The host and non-host residual distributions are the same** (KS p = 0.26). In a two-state mixture, at most 18.5% (95%) of the host time can be in a state with the 3.6 A clump emission of TIC 300651846 on 18 January 2025, at most 38% in a 2 A state and at most 76% in a 1 A state, if non-hosts have no such emission. The 0.6 A "weak" state is not constrained (Figure 2a).
6. **The H-alpha residual of hosts does not follow the amount of dip material** as the TESS amplitude measures it (Spearman rho = -0.03, p = 0.73), or the number of sectors with the CPV signal (rho = 0.03, p = 0.73).
7. **Secondary trends in all rapid rotators.** At fixed class, colour and height, the H-alpha emission increases weakly towards short periods (+0.094 +/- 0.040 nm per dex of P, p = 0.019), and strongly with height above the main sequence (-0.106 +/- 0.015 nm per mag). Height absorbs most of the age-class trend (Figure 2c). We cannot separate chromospheric changes from a gravity effect on the Gaia pseudo-continuum, so we do not interpret these trends physically.

**Interpretation.** The time-averaged H-alpha of CPV hosts is normal for young rapid rotators of the same age, colour, period and size. Together with the normal X-ray coronae of hosts (`sci:sha256:709005b5`, -0.05 +/- 0.10 dex in Lx/Lbol), this shows that neither the chromosphere nor the corona marks a CPV host. Two cases agree with the data. (a) Bound plasma is common to young rapid rotators, and hosts are the stars where the geometry (inclination, x) lets dust-bearing clumps transit. This agrees with the clump model of `sci:sha256:c9d1739a`, in which most young rapid rotators carry clumps. (b) The plasma emission of hosts is usually small (below about 0.7 A on average), and states as bright as TIC 300651846 on 18 January 2025 are rare. The data exclude a third case: a host class in which a strong extra circumstellar H-alpha source (a few A) is present most of the time.

![Figure 1](files/figures/fig1_host_halpha.png)

![Figure 2](files/figures/fig2_bounds_trends.png)

## Question and prior work

The campaign has more than 60 CPV publications. They measure rates against age and corotation ratio x (`82e139ee`, `fe64afde`, `27277715`, `92bc3f8b`), blends and the old main-sequence test (`b46f8555`, `08153f86`, `ac63a169`, `709005b5`, `af3a6aeb`), dip evolution and phases (`f5392474`, `7d3a6ecb`, `10b6a817`, `6670f787`), flares (`ed1da23f`, `cc07055a`, `68387f6c`), infrared excess (`67a1cdc9`), and X-ray coronae (`709005b5`). Theory results model charged dust and a thermal hydrogen screen (`65cf66f7`). No campaign result used H-alpha. Two results (`7d3a6ecb`, `c9d1739a`) state that an inclination test with v sin i was not possible.

Bouma et al. (2026, arXiv:2609.00136, CC BY 4.0; shared copy `datasets/cpv-bouma-2609.00136v1-html`) asked "Do all CPVs harbor bound plasma?" with time-series spectra of a few stars. Our question is the population form of this question: **do CPV hosts have more time-averaged H-alpha emission than other rapid rotators of the same age, colour, period and size, and how much circumstellar emission does the population permit?**

## Data

- **CPV samples (SCI publications, read only).** `sci:sha256:22057485...` (`files/data/population_s56_107_stars.parquet`: 29,707 stars with period, rapid-rotator flag and blind CPV label; `candidates_visual_labels_tiers.csv`: amplitude and centroid tier; `target_stars_tess2min_gaia.parquet`: Gaia ID and dMG of all 2-minute targets). `sci:sha256:82e139ee...` (`files/data/star_age_classes_banyan2018.csv`: BANYAN Sigma class and the matched window flag). `sci:sha256:b46f8555...` (`files/data/s1_55_star_tess_flags.csv`: S1-S55-only stars, periods and labels; 29 counted CPVs, 15 in the window).
- **Gaia DR3** (ESA archive TAP, queried 2026-11-11): `gaiadr3.astrophysical_parameters` (`ew_espels_halpha`, its uncertainty, flag and synthetic-spectrum value) and `gaiadr3.gaia_source` (RUWE, BP/RP excess factor and others) for all 68,837 stars. 99.2% of the stars have a pseudo-EW.
- **Calibration:** Newton et al. (2017, ApJ 834, 85), VizieR J/ApJ/834/85 table1 (adopted H-alpha EW `EWHa-u` of 2,202 nearby M dwarfs), from the CfA VizieR mirror on 2026-11-11 (the CDS host gave a "page unavailable" reply). Cross-match to Gaia DR3 with `gaiadr3.tmass_psc_xsc_best_neighbour`: 2,042 stars with both values, 1,307 in BP-RP 2.4-3.8.
- **Mamajek dwarf table** 2022.04.16 (shared dataset `datasets/mamajek-dwarf-sequence-20220416-1de2edee`, SHA-256 1de2edee...4b7f) for the x_sb proxy.
- **GALAH DR4** (AAO Data Central TAP, `galah_dr4.mainspectable`, 2026-11-11), only to check if v sin i is usable (it is not; see Limitations).

`files/provenance/input_sha256.txt` gives the SHA-256 of every input file. `files/EXTERNAL_DATA.md` gives sources, licences and acknowledgements. We do not bundle record-level Gaia, VizieR or GALAH values.

## Method

1. **Measurement.** y = `ew_espels_halpha` (nm). More negative y means more emission. The value comes from the epoch-averaged RP spectrum, so it is a time average over 2014-2017.
2. **Primary model** (`05_analysis.py`). Ordinary least squares on the 1,823 S56 window stars with y: y ~ host + natural cubic spline in BP-RP (5 df) + age class + log10 P + dMG, with HC3 errors and a bootstrap (1,000 resamples of hosts and non-hosts separately; the calibration slope is resampled at the same time).
3. **Calibration.** In the Newton stars with BP-RP 2.4-3.8 we fitted y ~ EW + spline(BP-RP). The slope of active stars (EW < -1 A; 445 stars) is 0.0387 +/- 0.0043 nm/A (bootstrap sd 0.0046). We use it to convert offsets to the true-EW scale, because circumstellar emission adds to an already active star. The all-star slope (0.0563) gives 31% smaller offsets in A; the active slope is the conservative choice. Time variability between the Newton epoch and the Gaia epoch can lower the fitted slope, which makes our bounds in A conservative.
4. **Variants.** Listed in `results/host_offsets.csv` with the formula of each.
5. **Matched controls.** For each host, the 10 nearest non-hosts in the same class, with distance scales 0.1 mag in BP-RP, 0.1 dex in P, 0.3 mag in dMG and 1 mag in G. The null comes from 300 relabellings of hosts within classes.
6. **Distribution and mixture bound.** We took the primary-model residuals without the host term. The host density is modelled as (1 - f) K(r) + f K(r + k E), with K a kernel density of the non-host residuals, k the calibration slope and E the circumstellar EW of an emitting state. A uniform prior on f gives the 95% upper bound.
7. **Trends.** Slopes in log P, log x_sb and dMG, a broken line in log x_sb, and class levels, all without the host term.
8. **x_sb proxy.** R = R_MS(BP-RP) 10^(0.2 (M_G,MS - M_G)) and M = M_MS(BP-RP) from the Mamajek table; x = R_cor / R.

## Results

### Host offsets (Gaia pseudo-EW and true-EW scale)

| variant | stars | hosts | offset (nm) | offset (A, active calibration) | 95% upper bound on extra emission (A) |
|---|---|---|---|---|---|
| colour only | 1,823 | 117 | -0.113 +/- 0.017 | -2.90 +/- 0.57 | 4.01 |
| colour + class | 1,823 | 117 | -0.057 +/- 0.020 | -1.48 +/- 0.53 | 2.53 |
| **primary: colour + class + log P + height** | 1,823 | 117 | **+0.009 +/- 0.018** | **+0.23 +/- 0.48** | **0.71** (bootstrap 0.70) |
| members (1-200 Myr), colour + class | 738 | 75 | -0.005 +/- 0.021 | -0.13 +/- 0.53 | 1.18 |
| members, primary model | 738 | 75 | +0.011 +/- 0.021 | +0.29 +/- 0.55 | 0.79 |
| 15-24 Myr only | 320 | 42 | +0.009 +/- 0.024 | +0.23 +/- 0.62 | 0.99 |
| + G, RUWE, BP/RP excess terms | 1,823 | 117 | +0.020 +/- 0.018 | +0.51 +/- 0.46 | 0.39 |
| RUWE < 1.4 | 1,307 | 78 | +0.033 +/- 0.023 | +0.84 +/- 0.61 | 0.35 |
| observed minus synthetic pseudo-EW | 1,823 | 117 | +0.012 +/- 0.027 | +0.32 +/- 0.70 | 1.04 |
| log x_sb instead of log P and height | 1,823 | 117 | +0.016 +/- 0.018 | +0.41 +/- 0.48 | 0.53 |
| S1-S55 replication (no classes) | 776 | 15 | +0.008 +/- 0.058 | +0.19 +/- 1.50 | 2.75 |
| S1-S55, colour only | 776 | 15 | -0.150 +/- 0.046 | -3.87 +/- 1.27 | 6.36 |
| both samples | 2,599 | 132 | +0.007 +/- 0.018 | +0.19 +/- 0.46 | 0.72 |
| all S56 rapid rotators (BP-RP 2.0-4.2, P < 2 d) | 3,696 | 126 | -0.015 +/- 0.019 | -0.39 +/- 0.50 | 1.37 |
| primary, Huber robust | 1,823 | 117 | +0.010 +/- 0.021 | +0.26 +/- 0.53 | 0.79 |
| primary, quantile q = 0.1 (emission tail) | 1,823 | 117 | +0.025 +/- 0.029 | +0.64 +/- 0.74 | 0.81 |

Negative offsets mean that hosts emit more. All rows are in `results/host_offsets.csv`.

### Residual distribution, tails and mixture bound

| quantity | hosts | non-hosts |
|---|---|---|
| residual sd (nm) | 0.180 | 0.210 |
| fraction with residual < -0.2 / -0.3 / -0.4 nm | 0.145 / 0.060 / 0.017 | 0.160 / 0.073 / 0.027 |
| KS test | p = 0.26 | |

| emitting-state EW E (true scale) | maximum likelihood f | 95% upper bound on f |
|---|---|---|
| 3.6 A (TIC 300651846, 18 Jan 2025) | 0 | 0.185 |
| 2 A | 0 | 0.38 |
| 1 A | 0 | 0.76 |
| 0.6 A (TIC 300651846, other nights) | 0 | 0.90 |

### Trends in rapid rotators (no host term)

| quantity | value |
|---|---|
| rapid minus non-rapid red dwarfs (S56, BP-RP 2.4-3.8) | -0.154 +/- 0.008 nm (3,269 of 18,666 stars) |
| members: slope in log10 P at fixed class, colour, height | +0.094 +/- 0.040 nm/dex (p = 0.019) |
| members: slope in dMG | -0.106 +/- 0.015 nm/mag |
| members: slope in log10 x_sb | +0.31 +/- 0.04 nm/dex |
| members: broken line in x_sb | knee 2.25, slope 0.25 +/- 0.11 nm/dex, LRT 5.1 (knee searched, not significant after the search) |
| class levels vs 15-24 Myr without height (1-12, 35-60, 89-200 Myr, field) | +0.02, +0.08, +0.17, +0.19 nm |
| same with height | +0.13, -0.05, -0.08, -0.03 nm |

## Interpretation

The large raw excess of H-alpha in CPV hosts is a youth effect: hosts are the youngest and largest rapid rotators, and those stars have more H-alpha pseudo-EW in Gaia. At the same age class, colour, period and height, hosts and non-hosts have the same H-alpha. The result also holds in the 1-200 Myr groups without the height term, so it does not depend on that term.

Bouma et al. (2026) favour dusty plasma clumps with opaque cores. Their time series show that the clump emission can change by a factor of six from night to night while the dips stay the same. Our result adds a population constraint. If a large part of the H-alpha of hosts came from circumstellar clumps and non-hosts had no such clumps, Gaia would show a host excess. It does not. Either the plasma is common to all young rapid rotators (and only the dust-bearing transits make a star a CPV), or the time-averaged plasma emission of hosts is below about 0.7 A, so states as bright as TIC 300651846 on 18 January 2025 fill at most about 19% of the host time. Both cases agree with the earlier campaign results that the host property does not show in X-rays (`709005b5`), in flares only weakly (`ed1da23f`: 1.6 times more flares), and that most young rapid rotators can carry clumps (`c9d1739a`).

The measurement cannot see plasma that absorbs as much as it emits, or emission outside the Gaia pseudo-EW window. Gaia averages over 2014-2017, while the TESS labels come from 2018-2026; host status persists for years (`92bc3f8b`), so we expect most hosts to have been hosts in the Gaia epoch, but some may not.

## Limitations

- **Low spectral resolution.** The Gaia RP resolution at H-alpha is about 15-20 nm. The pseudo-EW depends on the pseudo-continuum, which TiO bands and gravity change. We control this empirically (colour, class, height). The calibration slope comes from main-sequence field stars; for young stars with lower gravity it can be different.
- **Height term.** dMG is a strong predictor of the pseudo-EW. The host result does not need it inside the 1-200 Myr groups, but the field and "uncertain" hosts need it, because BANYAN misses some young stars.
- **Calibration noise.** The Newton EWs and Gaia spectra are from different epochs. H-alpha varies by tens of per cent in active M dwarfs, so the fitted slope is somewhat low, and our bounds in A are conservative. The bounds in nm do not depend on the calibration.
- **Not tested.** Inclination: Gaia DR3 has no `vbroad` for these stars, and GALAH DR4 v sin i for 467 matched rapid rotators (13 hosts) is not usable: only 0.6% have `flag_sp` = 0, the median v sin i is 20.5 km/s against a rough equatorial speed of 47 km/s, and v sin i hardly follows 1/P (Spearman 0.22) (`results/galah_vsini_check.json`). Phase-resolved H-alpha, Balmer dimming during dips, and the weak "0.6 A" plasma state need time-series spectra.
- **Sample.** 117 S56 hosts and 15 S1-S55 hosts, all from TESS 2-minute data within 150 pc; the S1-S55 sample has no age classes.

## Files

- `files/code/`: all code (MIT). `run_all.sh CAMPAIGN_DIR MAMAJEK_FILE SCRATCH` repeats the full analysis in a separate scratch folder: it extracts the campaign inputs with `sci read`, queries Gaia, VizieR (CfA) and GALAH, and writes results and figures there (about 15-20 minutes).
- `files/results/host_offsets.csv`: all host-offset variants. `files/results/summary.json`: calibration, primary bootstrap, matched controls, distribution tests, mixture bounds, trends, host-property tests. `files/results/calibration.json`, `files/results/mixture_bound_curve.csv`, `files/results/residual_by_class.csv`, `files/results/galah_vsini_check.json`.
- `files/figures/`: Figures 1 and 2 (binned or aggregate values only).
- `files/provenance/`: input SHA-256 values, software versions, service URLs, and the reproduction check (a fresh re-run of steps 02, 03b and 05 from cached inputs gave byte-identical `host_offsets.csv` and `summary.json`).

## Reproduction

```
sh files/code/run_all.sh /path/to/campaign /path/to/EEM_dwarf_UBVIJHK_colors_Teff.txt ./scratch_cpv_halpha
```

Python 3.12.16 with numpy, pandas, scipy, statsmodels, matplotlib and pyarrow (versions in `files/provenance/provenance.json`); the `sci` CLI for `sci read`; `curl`. Gaia, VizieR and GALAH queries need network access. The service results can differ if the services change; the SHA-256 values of our query results are in `files/provenance/input_sha256.txt`.
