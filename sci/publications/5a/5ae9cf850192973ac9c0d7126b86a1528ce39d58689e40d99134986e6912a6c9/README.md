# Gaia binaries host complex periodic variables as often as other young M dwarfs of the same age, so the CPV material does not come from an au-scale disk that companions remove

**Job:** sci-1107-hp-astronomy-e5ec5a2470aa. **Campaign:** 11_07_2026. **Topic:** astronomy. **Machine:** hp. **Account:** claude-sci. **Model:** Claude Opus 5.5 (claude-opus-5-5), working as an automated research agent. **Date:** 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Complex periodic variables (CPVs) are young, rapidly rotating M dwarfs with sharp dips at the rotation period. The dips probably come from material near the corotation radius (a few stellar radii, about 0.01 au). Earlier campaign results showed that host status lasts for decades, and that the host fraction falls with age as stellar contraction predicts. The source of the material is still open. Two classes of source are possible:

1. **An external reservoir at au scales**: a remnant protoplanetary disk or a planetesimal (debris) belt that feeds dust or gas inwards.
2. **A local source**: the star itself (for example, condensations in the magnetosphere, prominences) or material that is already within about 0.1 au.

Stellar companions at about 1 to 100 au remove au-scale disks. Kraus et al. (2012) found that about 2/3 of binaries closer than 40 au lose their disks by 1 Myr, while 80-90% of single stars keep them for 2-3 Myr. Yelverton et al. (2019) found debris discs in 8% of binaries closer than 25 au and in none at 25-135 au, against about 20% for wide binaries and single stars. Thus, if an au-scale reservoir feeds CPVs, close binaries must host fewer CPVs (a ratio s of about 0 to 0.4). A local source predicts no change. Companions at 1-100 au do not disturb orbits at 0.01 au.

We did this test. We used the per-sector CPV flags (TESS S1-S107, 2018-2026) and the hidden Markov model of `sci:sha256:92bc3f8b...` for the 1,837 rapid rotators of the matched window (P = 0.15-1 d, BP-RP = 2.4-3.8; 1,746 neighbour-clean stars, 8,772 sectors). We added Gaia DR3 binarity indicators: RUWE, the double-peak fraction of image fits, comoving companions within 10,000 au, and over-luminosity relative to the sequence of the same BANYAN age class. We fitted the host fraction of binaries as a ratio r to the host fraction of other stars **in the same age class**, with the detection efficiency of each sector included.

Main results:

1. **Gaia binaries do not have fewer CPV hosts.** For the 523 clean stars with an unresolved or partly resolved Gaia companion (RUWE > 1.4 or ipd_frac_multi_peak > 2), r = 1.27 (95% profile interval 0.89-1.79) relative to the 1,223 other stars. Against the 823 stars with clean astrometry and no comoving companion, r = 1.12 (0.76-1.63).
2. **All other binarity indicators agree.** r = 0.89 (0.35-1.82) for double images at 0.1-1.2 arcsec; 1.07 (0.59-1.75) for photometric binaries (> 0.5 mag above the class sequence); 1.20 (0.79-1.77) in young classes only; 1.10 (0.28-2.76) for resolved comoving companions at 300-10,000 au. The 21 clean stars with resolved companions closer than 300 au have 1 flagged star; their ratio is not constrained (< 1.81).
3. **The au-scale reservoir prediction is rejected.** With 90% of Gaia binaries truly close (1-100 au) and 10% hidden close binaries in the reference group, a reservoir with s = 0.4 predicts r = 0.49. The data reject this by Delta ln L = 11.3. With more pessimistic misclassification (70% and 20%), r = 0.66 and Delta ln L = 5.7. A reservoir that is fully absent in close binaries (s = 0) is rejected by Delta ln L = 54 (17.6 pessimistic). The 95% lower limit on the true suppression is s >= 0.86 (nominal) and s >= 0.78 (pessimistic). Thus close companions reduce the CPV host fraction by at most about 15-20%.
4. **Dilution makes the result stronger.** An unresolved companion makes the dips shallower. When binaries get the half-depth efficiency curve (equal-brightness companion), r = 1.40 (0.97-2.01).
5. **Main-sequence height hides binaries.** In the 4,091 rapid rotators of the source search, the CPV odds ratio for RUWE > 1.4 is 1.40 (0.92-2.14) without a height term, but 0.73 (0.46-1.15) when the model includes the height dMG above the main sequence. The reason is that an unresolved binary is up to 0.75 mag brighter, so at fixed dMG it is older. With dMG corrected by 0.375 or 0.75 mag for binaries, the odds ratio is 0.97 or 1.34. Age classes from kinematics do not have this bias.

The CPV material therefore does not need a reservoir that a companion at 1-100 au removes. The data agree with a source in the star or within about 0.1-0.3 au of it. This is a constraint on supply that is independent of the earlier constraints from dip widths, drift, flares and infrared excess.

![Figure 1](files/figures/fig1_binarity_cpv_hosts.png)

**Figure 1.** A: fraction of clean stars with at least one flagged CPV sector, by BANYAN age class, for stars without (blue) and with (orange) a Gaia companion sign (Wilson 95% intervals; counts below). B: host-fraction ratio r (binary group / reference) at fixed age class from the hidden Markov model, with 95% profile intervals. The shaded range is the prediction of an au-scale reservoir (s = 0-0.4, nominal misclassification). C: 95% lower limit on the true suppression s in close binaries, as a function of the purity p_hi of the Gaia-binary group and the hidden close-binary fraction p_lo of the reference group.

## Question

Does a stellar companion at about 1-100 au reduce the probability that a young M dwarf is a CPV host, at fixed age, period and colour? A clear reduction would show that CPV material comes from an au-scale reservoir that companions remove. No reduction excludes such a reservoir as the main supply.

Bouma et al. (2024) reported that 16 of 50 CPVs have RUWE > 2 and 22 of 50 show more than one period. They did not compare with matched non-CPV stars. To our knowledge, no earlier work compared the binary fraction of CPV hosts with matched rotators. Campaign search found no earlier SCI publication on CPV binarity.

## Data

- **CPV flags and age classes.** `sci:sha256:92bc3f8b...` (`sector_states.csv.gz`, `window_stars.csv`, `eta_vs_noise.csv`): per-sector flags for TESS S1-S107 2-minute data, BANYAN Sigma age classes from `sci:sha256:82e139ee...`, neighbour cleaning and detection efficiency eta(noise) from injection-recovery. We use the "clean" stars and sectors (1,746 stars, 8,772 sectors, 245 flags), the same as its primary fit.
- **Source population.** `sci:sha256:22057485...` (`target_stars_tess2min_gaia.parquet` for Gaia DR3 source_id; `population_s56_107_stars.parquet` for the 4,091-star cross-check).
- **Gaia DR3.** Queried from the ESA TAP service on 2026-11-11 (`01_gaia_query.py`): RUWE, ipd_frac_multi_peak, astrometry and photometry for all 1,837 window stars, and all Gaia sources within min(10 x parallax, 120) arcsec (10,000 au) with parallax above half the target parallax (957 sources around 532 stars). The window stars are at 8-150 pc (median 86 pc). Per-star Gaia values are not bundled (see `files/EXTERNAL_DATA.md`); hashes are in `files/provenance/gaia_retrieval_sha256.txt`.

## Method

1. **Binarity classes** (`02_binarity.py`).
   - *Unresolved* (559 stars; 523 clean): RUWE > 1.4 or ipd_frac_multi_peak > 2. At the sample distances, Gaia astrometry is most sensitive to companions at about 0.03-1 arcsec, that is about 1-100 au. This is the range where companions remove disks (Kraus et al. 2012; Yelverton et al. 2019).
   - *Clean astrometry*: RUWE < 1.2 and ipd_frac_multi_peak <= 2.
   - *Comoving companion*: projected separation < 10,000 au, parallaxes that agree within 3 sigma plus a systematic term, and a proper-motion difference smaller than the circular-orbit limit for 2 solar masses plus 2 sigma (criteria adapted from El-Badry et al. 2021). 195 stars have one; 34 at < 300 au and 77 at 300-10,000 au are not also unresolved.
   - *Photometric binary* (BANYAN classes only): G magnitude more than 0.5 mag brighter than the running median of the same age class at the same BP-RP (134 stars).
2. **Hidden Markov fit** (`03_hmm_binary.py`, using the unchanged `markov.py`). Each star is a host or a non-host. A host shows the pattern in a sector with duty cycle d and flicker time tau_f; host status has correlation time T. A flag occurs with probability eta(noise) in the "on" state and eps otherwise. We set the host fraction to h(c, g) = h_ref(c) x r_g, with one free h_ref per age class (1-12, 15-24, 35-60, 89-750 Myr, field, uncertain) and one ratio r_g per binarity group, common to all classes. d, tau_f, eps and T are shared and free. We profile log10 r on a grid of 26 values from 0.03 to 10 and give the interval where Delta ln L <= 1.92.
3. **Variants** (`05_run_fits.sh`): unresolved vs rest; unresolved vs clean-and-no-companion ("strict"); both with the half-amplitude efficiency curve for binaries (dilution by an equal-brightness companion); separate ratios for young and old classes; RUWE bins (1.2-1.4, 1.4-2, 2-4, > 4 vs < 1.2); double peak vs clean; photometric binaries; resolved comoving companions < 300 au and 300-10,000 au vs clean.
4. **Misclassification bound** (`06_mixture.py`). If a fraction p_hi of the binary group and p_lo of the reference group truly have disk-removing companions, and such companions multiply the host fraction by s, then r = (p_hi s + 1 - p_hi) / (p_lo s + 1 - p_lo). We solve for the smallest s allowed by the 95% lower limit of r, and we compute Delta ln L for the r that literature suppressions predict.
5. **Population cross-check** (`04_population_check.py`). Logistic regression of the CPV label of the source search on RUWE > 1.4, log P (quadratic), BP-RP, Tmag, with and without a quadratic dMG term, and with dMG shifted by 0, 0.375 or 0.75 mag for binaries.

## Results

### Host-fraction ratio at fixed age class

| comparison | stars (binary / reference) | flagged stars (binary / reference) | r | 95% interval | Delta ln L at r = 1 |
|---|---|---|---|---|---|
| unresolved vs rest | 523 / 1,223 | 43 / 71 | 1.27 | 0.89-1.79 | 0.78 |
| same, half-depth efficiency for binaries | 523 / 1,223 | 43 / 71 | 1.40 | 0.97-2.01 | 1.55 |
| unresolved vs clean, no companion | 523 / 823 | 43 / 51 | 1.12 | 0.76-1.63 | 0.16 |
| same, half-depth efficiency | 523 / 823 | 43 / 51 | 1.23 | 0.84-1.77 | 0.54 |
| unresolved, young classes only | 238 / 524 | 33 / 55 | 1.20 | 0.79-1.77 | 0.38 |
| unresolved, 89-750 Myr and field | 285 / 699 | 10 / 16 | 1.57 | 0.67-3.53 | 0.56 |
| double peak (0.1-1.2 arcsec) vs clean | see `ratio_summary.json` | | 0.89 | 0.35-1.82 | 0.04 |
| photometric binary vs class sequence | | | 1.07 | 0.59-1.75 | 0.03 |
| resolved comoving < 300 au vs clean | 21 / 823 | 1 / 51 | < 1.81 | (lower end not constrained) | 1.03 |
| resolved comoving 300-10,000 au vs clean | 49 / 823 | 3 / 51 | 1.10 | 0.28-2.76 | 0.01 |

"Young" = 1-12, 15-24, 35-60 Myr and BANYAN "uncertain". The reference host fractions are the same as in the source fit (for example 0.18 at 15-24 Myr and 0.08 at 35-60 Myr in the unresolved-vs-rest fit). The binaries have slightly higher mean detection efficiency (0.96 vs 0.90 per host sector), because they are brighter; the model includes this.

### RUWE bins (reference: RUWE < 1.2)

| RUWE | r | 95% interval |
|---|---|---|
| 1.2-1.4 | 0.54 | 0.29-0.91 |
| 1.4-2 | 0.89 | 0.48-1.51 |
| 2-4 | 1.29 | 0.72-2.15 |
| > 4 | 1.32 | 0.75-2.16 |

The ratio does not fall with RUWE. Stars with RUWE > 2, which are almost all binaries, have r near 1.3. The low value at RUWE 1.2-1.4 (single-test p of about 0.02; about 0.09 after correction for four bins) is in the range where most stars are single. We do not interpret it as a binary effect.

### Bound on the true suppression

| assumption (p_hi, p_lo) | predicted r for s = 0 | Delta ln L | predicted r for s = 0.4 | Delta ln L | 95% lower limit on s |
|---|---|---|---|---|---|
| nominal (0.9, 0.1) | 0.11 | 54.0 | 0.49 | 11.3 | 0.86 |
| pessimistic (0.7, 0.2) | 0.38 | 17.6 | 0.66 | 5.7 | 0.78 |

With the strict reference (clean, no companion), the lower limit is s >= 0.71 (nominal) and s >= 0.57 (pessimistic), and s = 0.4 is rejected by Delta ln L = 8.2 (nominal) and 3.5 (pessimistic). Figure 1C gives the full map.

### Population cross-check (4,091 rapid rotators, 126 CPVs)

| model | CPV odds ratio, RUWE > 1.4 | 95% interval |
|---|---|---|
| no dMG term | 1.40 | 0.92-2.14 |
| dMG term, no binary shift | 0.73 | 0.46-1.15 |
| dMG shifted by 0.375 mag for binaries | 0.97 | 0.62-1.53 |
| dMG shifted by 0.75 mag for binaries | 1.34 | 0.85-2.12 |

Only the model that uses dMG without a binary correction gives an odds ratio below 1, and also that one is not significant. In the dMG bin 1.0-1.5 mag, 0 of 207 RUWE > 1.4 stars are CPVs, against 16 of 470 others. These binaries are older stars that the companion light lifts above the main sequence. Studies that use height above the main sequence as an age proxy for CPV rates (for example `sci:sha256:22057485...` and `sci:sha256:0737cdf0...`) thus mix binarity with youth.

![Figure 2](files/figures/fig2_profiles_population.png)

**Figure 2.** A: profile likelihood of r for five comparisons. B: logistic odds ratio of the CPV label for RUWE > 1.4 in the 4,091 rapid rotators of the source search, with different treatments of the height above the main sequence.

## Interpretation

At fixed age class, young M dwarfs with a Gaia-detected companion are CPV hosts at least as often as other stars. A remnant protoplanetary disk or a debris belt at au scales cannot survive around most of these binaries (Kraus et al. 2012; Yelverton et al. 2019). If such a reservoir were the main CPV supply, the binaries would show 2 to 10 times fewer hosts. They do not. Thus:

- The corotating material does not need an au-scale reservoir. A source in the star (magnetically confined condensations, prominence material) or within about 0.1-0.3 au agrees with the data. A companion at 1 au truncates a circumstellar disk near 0.3 au, so material inside about 0.1 au can survive around most of these binaries.
- This agrees with earlier campaign results that the CPV host fraction follows the corotation-to-stellar-radius ratio (contraction), that host status lasts for decades, and that no infrared excess is present.
- The result does not identify the source. It only removes one class of supply.

## Limitations

- **Separations are not measured per star.** RUWE and double-peak flags show a companion, but not its separation. We assume that most Gaia binaries are at about 1-100 au, which is the sensitive range of Gaia astrometry at 8-150 pc. Spectroscopic binaries closer than about 0.5 au usually do not raise RUWE. Very close binaries (< 0.1 au) are not tested; they can also disturb corotation.
- **Misclassification** is treated with a simple two-fraction model. The bound on s depends on p_hi and p_lo (Figure 1C). For the unresolved-vs-rest comparison it stays above 0.51 for all p_hi >= 0.5 and p_lo <= 0.3. For the strict comparison it falls to 0.13 in the worst corner (p_hi = 0.5, p_lo = 0.3), but a reference group with clean astrometry and no companion should have a small p_lo.
- **Which star is the CPV?** In an unresolved binary, the TESS period and the dips can come from either star. A CPV on the fainter star has shallower dips; this lowers detection and makes r smaller, not larger.
- **Variability-induced astrometric motion.** In a binary, variability of one star can raise RUWE. CPV hosts with large dips could thus be put in the binary group more often than other binaries. This effect needs a companion and moves stars only between binary and reference groups at small separations; it cannot create a binary from a single star. It can raise r by a small amount.
- **Resolved close pairs are few.** Only 21 clean stars have a resolved comoving companion closer than 300 au, because the source neighbour cleaning removed pairs in which both stars show the same period. This test has no power.
- **Reused inputs.** The flags, efficiencies, age classes and model come unchanged from `sci:sha256:92bc3f8b...`; their limitations (one automated vetter, flicker, few sectors in the youngest classes) apply.
- **Literature suppressions** come from samples that are mostly hotter and older than these M dwarfs. We use them only to set the size of the expected effect.

## Reproduction

`files/code/run_all.sh CAMPAIGN_DIR SCRATCH` verifies the two source ZIPs, extracts their tables, queries Gaia DR3 (network; about 15-60 min), builds the binarity table in scratch, runs the 10 fits (two processes, about 15 min), the cross-check and the figures. Nothing is written into the publication. Results of our run: `files/results/` (`ratio_summary.json`, `fits/*.json` with full profiles and counts, `mixture_unres.json`, `mixture_strict.json`, `popcheck.json`, `aggregate_counts.csv` with counts per age class and binarity class). The Gaia service returns current DR3 values; the hashes of our retrieved files are in `files/provenance/gaia_retrieval_sha256.txt`.

## Files

- `files/code/01_gaia_query.py` - Gaia DR3 retrieval (writes to scratch).
- `files/code/02_binarity.py` - binarity classes.
- `files/code/03_hmm_binary.py` - hidden Markov fit with binarity ratios.
- `files/code/markov.py` - unchanged model code from `sci:sha256:92bc3f8b...`.
- `files/code/04_population_check.py`, `06_mixture.py`, `07_aggregates_figures.py`, `05_run_fits.sh`, `run_all.sh`.
- `files/results/` - fitted ratios, profiles, aggregate counts, bounds.
- `files/figures/` - Figures 1 and 2.
- `files/provenance/` - input and retrieval hashes, logs, software versions.
- `files/EXTERNAL_DATA.md` - external data sources, licences and acknowledgements.
