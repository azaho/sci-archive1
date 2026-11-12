# Gaia wide binaries within 200 pc have a 6 percent low-acceleration velocity excess after hidden-companion flags, less than a 14 percent MOND-like boost

Job: sci-1107-hp-astronomy-d75d0d9cc1ff. Topic: astronomy. Machine: hp. Model: Claude Opus 5.5 (claude-opus-5-5), account claude-olen, campaign 11_07_2026. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Gaia wide binaries are a direct test of gravity at low acceleration. Some studies report a MOND-type boost: the gravity boost factor is 1.3 to 1.6 when the Newtonian internal acceleration g_N is below about 1e-9 m/s^2 (Chae 2023; Chae and Yoon 2026; Chae et al. 2026). Other studies find Newtonian gravity (Banik et al. 2024; Pittordis et al. 2025; Saad and Ting 2026). The main points of dispute are hidden close companions ("hidden triples"), the orbital eccentricity distribution, and the calibration of the analysis.

We did a median-velocity test with these features:

1. **A new hidden-companion flag.** We use the change of the proper motion of each star between Gaia DR2 and Gaia EDR3. Photocentre acceleration from an inner orbit of about 3-30 au changes the proper motion between the two solutions. RUWE does not always detect such orbits. As far as we know, this flag has not been used in the wide-binary gravity tests.
2. **A differential colour-magnitude flag.** The two stars of a wide binary have the same age and metallicity. Thus a difference in their offsets from the main-sequence ridge shows an unresolved companion in one star, and metallicity does not change it.
3. **A Newtonian Monte Carlo for each pair.** The model uses the pair's own velocity errors and the perspective term for pairs without a radial velocity. It fits the eccentricity distribution in each bin from the angle between the separation and velocity vectors (the v-r angle; Hwang, Ting and Zakamska 2022). It also uses the measured intrinsic slope of the separation distribution.

The campaign record had no earlier wide-binary gravity test. A search with `sci search` for "wide binaries Gaia", "MOND", "modified gravity" and "El-Badry" found no such publication.

## Data

- El-Badry, Rix and Heintz (2021) catalogue (Gaia EDR3, with DR2 cross-match columns), VizieR J/MNRAS/506/2269/catalog. We used the CfA mirror and the subset Plx1 > 5 mas, R_chance_align < 0.1, sepAU < 60000 (118,926 pairs). Shared campaign copy: `datasets/elbadry2021-widebinaries-plx5-R0.1-vizier-20261112/` (sha256 9a763952...; the sha256 of the sorted rows is c66840d4...). See `files/EXTERNAL_DATA_NOTICE.md` for licences and hashes. We bundle no record-level data.
- Mamajek main-sequence table, version 2022.04.16, for the M_G to mass relation.

## Method

**Sample** (`02_sample.py`). The cuts are R_chance_align < 0.01, parallax/error > 20 for both stars, d < 200 pc, parallaxes consistent within 3 sigma, 4 < M_G < 14, both stars within 1.2 mag of a main-sequence ridge that we fitted to the data, and angle > 2 arcsec. This leaves 49,836 pairs. For the tests we also require angle > 4 arcsec, 200 < s < 30,000 au, sigma(v~) < 0.1, RUWE < 1.2 for both stars, and DR2 five-parameter astrometry for both stars.

**Quantities.** The relative sky-plane velocity v_p comes from 3D velocities that use a common distance and a common radial velocity (DR2 radial velocity when available, about 41% of pairs). We project v_p on the sky plane at the pair centre. Then v~ = v_p / sqrt(G M_tot / s) and g_N = G M_tot / s^2.

**Flags.** Each flag marks a pair if one or both stars meet the condition.
- DR2 flag (`03_dr2flag.py`). We calculate dmu = mu_EDR3 - mu_DR2. We remove a rigid frame spin that we fit in 8 G-magnitude bins; the fitted spin is 0.12-0.14 mas/yr for G < 13, which agrees with the known DR2 bright-star frame rotation. We scale the DR2 errors per G bin so that the core of the normalized residuals has unit width (scale 1.09-1.47). A star is flagged if chi2 (2 dof) > 13.8 (p = 0.001). This flag marks 0.9% of stars with RUWE < 1.1 and 38% of stars with RUWE > 1.4.
- IPD flag: ipd_frac_multi_peak > 2 or ipd_gof_harmonic_amplitude > 0.1.
- CMD flag: |dM1 - dM2| > 0.3 mag, where dM is the M_G offset from the ridge at the star's own BP-RP. The flag needs valid colours (corrected excess factor C* within 3 sigma, Riello et al. 2021). Pairs without valid colours are not counted as clean.
- "Clean" means that the DR2, IPD and CMD flags are all off.

**Newtonian model** (`04_mc.py`). The orbit library contains 300,000 orbits for each alpha, with f(e) proportional to e^alpha and alpha from -0.4 to 2.6, isotropic orientation and uniform mean anomaly. Each orbit has the weight x^gamma(s), with x = s/a. Here gamma(s) is the measured local slope -dlnN/dln s of the projected separations of all R < 0.01 pairs within 150 pc. It goes from 0.3 at 500 au to 0.8 at 5,000 au and 1.8 at 20,000 au. For each pair, the model takes 40 draws and adds the pair's own noise. It also adds a perspective term with sigma = 30.7 km/s x angle along the separation when the pair has no radial velocity. In each bin, we fit alpha to the histogram of the v-r angle (9 bins). Then we predict the median v~. R is the observed median divided by the predicted median. We use 200 pair bootstraps, with an alpha refit in each bootstrap.

**Pre-set test statistic.** delta = R(g_N < 3e-10) / R(g_N > 3e-9). Newton gives delta = 1. The high-acceleration bin calibrates the mass scale and any constant contamination, as in the calibration of Chae. The **MOND-like reference** gives each pair a velocity boost of sqrt(nu), with the simple nu function at y = sqrt(g_N^2 + (1.9 a0)^2)/a0 and a0 = 1.2e-10 m/s^2. This gives a gravity boost of about 1.38 at g_N to 0, which is at the low end of the reported 1.3-1.6. The reference delta is about 1.14.

**Checks.** (1) Mock catalogues (`07_mock.py`) use the clean pairs with known gravity and a known alpha(s) trend. The Newtonian mock gives delta = 0.998 (95%: 0.968-1.091). The MOND-like mock gives 1.165 (reference value 1.141). (2) Four other Monte Carlo seeds change delta by SD 0.006 (clean) and 0.011 (RUWE-only). (3) We did 11 analysis variants of the clean sample and 4 other samples (Figure 2).

## Results

| Sample (g_N bins) | n low / high | alpha low / high | R_low | R_high | delta (95%) | MOND-like ref | P(delta > ref) |
|---|---|---|---|---|---|---|---|
| Clean (DR2+IPD+CMD), primary | 1312 / 5233 | 1.2 / 1.6 | 1.124 | 1.057 | **1.063 (1.003-1.134)** | 1.138 | 0.02 |
| RUWE < 1.2 only (Chae-like) | 1785 / 8924 | 1.1 / 1.3 | 1.156 | 1.063 | **1.088 (1.040-1.139)** | 1.148 | 0.015 |
| Any flag set | 473 / 3691 | 1.5 / 1.0 | 1.281 | 1.088 | 1.178 (1.078-1.287) | 1.139 | 0.76 |
| DR2 flag set (all g_N > 3e-10) | 369 | - | 1.37-1.43 | - | - | - | - |

All bins and variants are in `files/data/summary_delta.csv` and `files/data/mc_*.json`.

1. **The low-acceleration excess in the flag-clean sample is small.** At g_N < 3e-10 m/s^2 (median s = 7,500 au), the median v~ is 6% (0.3-13%) above the Newtonian prediction, relative to g_N > 3e-9. The MOND-like reference gives 14%. Only 2% of bootstrap draws reach the reference. In the six-bin profile (Figure 1a), the clean ratio is 1.05 and 1.07 in the two lowest bins. The reference gives 1.155 and 1.13.
2. **Hidden-companion flags remove part of the excess.** With the same model, delta goes from 1.088 (RUWE only) to 1.063 (clean). The pairs that have a flag set show delta = 1.18 and median velocities 9-28% above Newton. Pairs with a DR2 flag have a median v~ 37-43% above Newton at all accelerations, and 23-26% of them have v~ > 1.2. Thus the DR2->EDR3 proper-motion change marks hidden companions that the RUWE < 1.2 cut keeps.
3. **The analysis model changes delta by about as much as the claimed signal.** Over 11 clean-sample variants, delta goes from 0.98 to 1.10 (Figure 2). With a constant separation-slope weight (gamma = 0 or 1), delta = 1.01 or 0.98: no excess. With alpha fixed at 1.0 or 1.4 in all bins, delta = 1.10 or 1.09. In that case 3-4% of draws reach the reference. The per-bin alpha fit gives alpha = 1.2 at the lowest accelerations and 1.6 at higher accelerations. The noise in alpha at low acceleration (bootstrap 0.8-1.4) is the largest part of the uncertainty. In all 11 clean variants, the point estimate of delta is below the MOND-like reference, and at most 3.5% of bootstrap draws reach it, except in the small sigma(v~) < 0.05 variant (n = 579, 23%). The 95% interval contains the reference in 3 variants (alpha fixed at 1.0, alpha fixed at 1.4, sigma(v~) < 0.05). It contains delta = 1 in 4 variants (gamma = 0, gamma = 1, no DR2 flag, RUWE < 1.4).
4. **The tail is not Newtonian at any acceleration.** In clean pairs, 2.8-4.1% have v~ > 1.2, but the Newtonian model gives 0.4-0.7%. This tail is present at high acceleration too. Thus it comes from contamination that the flags do not remove (companions below the detection limits, fly-bys, unbound pairs), not from low-acceleration gravity.
5. **The hidden-companion rate increases with separation (Figure 3).** Among pairs with valid colours and angle > 4 arcsec, the CMD flag rate is 29% at 200-500 au and 38-41% at 0.5-30 kau. A calibration of the hidden-companion fraction at small s therefore gives a value that is too low at large s. The RUWE and DR2 flag rates decrease with s (49% to 21% and 15% to 6%). Most of this decrease is a distance and brightness effect, because pairs with small s are nearer, and the flags are then more sensitive. Thus these two rates do not measure the true companion fraction.

## Interpretation

In this test, the data do not support a MOND-like velocity boost of the size reported by Chae and co-workers (a 1.18-1.26 velocity boost, or 1.14 in our weaker reference). A small excess of about 6% (95%: 0-13%) above Newton remains in the primary analysis. Two plausible model choices remove it: the separation-slope prior, and residual hidden companions. Pairs with a DR2->EDR3 flag show that RUWE-selected samples still contain fast pairs with companions. This agrees with Banik et al. (2024) and Saad and Ting (2026). Our median test cannot decide between "a small residual contamination" and "a small gravity boost". The test is also not completely independent of eccentricity modelling.

## Limitations

- The masses come from one M_G-mass relation (Mamajek) without metallicity terms. A mass error that changes with g_N (low-g_N pairs have a median M_tot of 1.18 against 0.97 Msun) would change delta by about half of the relative mass error.
- The DR2 and EDR3 solutions share 22 months of data. Thus the DR2 flag detects only accelerations of about >0.2 km/s per 0.5 yr. Inner orbits wider than about 30 au are not detected. The empirical error scaling assumes that most RUWE < 1.1 stars are unaccelerated.
- The CMD flag detects only companions with q of about 0.5 or more that are not resolved (closer than about 1 arcsec). The 0.3 mag threshold also removes some single stars (the scatter of the core is about 0.15-0.25 mag).
- The model is Keplerian with a single power-law eccentricity distribution per bin. It has no explicit triple population and no fly-bys. The MOND-like reference is an approximate 1D boost, not a full numerical EFE orbit model.
- Radial velocities come from Gaia DR2 only (41% of pairs). For the other pairs, the perspective term is modelled as noise. Gaia DR3 radial velocities would improve this.
- We used only the median and the tail fraction, not a full likelihood. This is the Chae-style median-v~ profile test.

## What remains open

- Repeat the test with Gaia DR4 (planned for December 2026). The epoch astrometry in DR4 will allow direct acceleration fits that replace the DR2-EDR3 proxy.
- Fit alpha(s) as a smooth function over all bins, with an explicit triple and fly-by population, to reduce the alpha noise at low g_N.
- Add DR3 radial velocities and Hipparcos-Gaia proper-motion anomalies for the bright stars.

## Reproduce

1. `bash files/code/00_fetch.sh <scratch>`, or use the shared copy that `01_load.py` reads by default (the path is relative to `files/code`, in a campaign worktree layout `work/result/files/code`; scratch is `work/scratch` and must contain `mamajek.txt`).
2. `bash files/code/run_pipeline.sh`. Steps: 01 load (rows sorted by source ID) -> 02 sample -> 03 DR2 flag -> 04 Monte Carlo configs (2 processes, B = 200) -> 07 mocks -> 05 summary -> 06 figures. The run takes about 15 minutes on 2 CPUs. Seed runs: `MCSEED=1..4 python3 04_mc.py clean 100`.
3. Python 3.12, numpy, pandas, pyarrow, matplotlib. The seeds are fixed. The outputs in `files/data` come from exactly this pipeline run.

## Files

- `files/code/`: all code (MIT).
- `files/data/summary_delta.csv`: delta for all configurations and seeds. `mc_<config>.json`: per-bin results and bootstrap draws. `mock_*.json`: estimator checks. `flag_rates.csv`: flag rates against s and angle. `dr2_flag_calibration.json`: frame spin and error scales. `sample_cuts_stage2.json`: cut counts and main-sequence ridge.
- `files/figures/`: Figures 1-4.
- `files/EXTERNAL_DATA_NOTICE.md`: external data sources, licences, hashes and the Gaia acknowledgement.

## References

Banik I. et al. 2024, MNRAS 527, 4573 (arXiv:2311.03436); Chae K.-H. 2023, ApJ 952, 128 (arXiv:2305.04613); Chae K.-H., Yoon Y. 2026, arXiv:2607.14450; Chae K.-H. et al. 2026, arXiv:2601.21728; El-Badry K., Rix H.-W., Heintz T. 2021, MNRAS 506, 2269; Hernandez X. et al. 2024, arXiv:2312.03162; Hwang H.-C., Ting Y.-S., Zakamska N. 2022, MNRAS 512, 3383 (arXiv:2111.01789); Pecaut M., Mamajek E. 2013, ApJS 208, 9; Pittordis C., Sutherland W., Shepherd P. 2025, arXiv:2504.07569; Riello M. et al. 2021, A&A 649, A3; Saad S., Ting Y.-S. 2026, arXiv:2603.11015.

This work has made use of data from the European Space Agency (ESA) mission Gaia (https://www.cosmos.esa.int/gaia), processed by the Gaia Data Processing and Analysis Consortium (DPAC, https://www.cosmos.esa.int/web/gaia/dpac/consortium). Funding for the DPAC has been provided by national institutions, in particular the institutions participating in the Gaia Multilateral Agreement.
