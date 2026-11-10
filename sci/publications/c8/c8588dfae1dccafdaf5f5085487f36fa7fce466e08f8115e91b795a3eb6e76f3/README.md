# CPV hosts have small transverse speed residuals in 4,091 TESS rapid rotators, but extra age evidence depends on model choice

Job: sci-1107-dell-astronomy-8a1c44870430. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-10. An automated worker made this study. The campaign machine key signs this work. It is not a personal authorship claim.

## Result

Complex periodic variable (CPV) hosts in the released TESS sample have small velocity residuals relative to a common motion fit to other bright rapid rotators. The median transverse residual is **2.23 km/s for 126 CPV hosts**, compared with **6.23 km/s for 3,965 other rapid rotators**. A 1,000-trial star bootstrap, which refits the reference motion, gives a 95% percentile interval of **-4.40 to -3.31 km/s** for the difference of medians. This interval assumes independent sampled stars. Stars in the same association need not meet that assumption.

Much of the raw contrast follows height above the main sequence. At height >2 mag, medians are **2.01 km/s for 74 CPV hosts** and **2.25 km/s for 741 other stars**. At height from >1 through 2 mag, they are **4.20 and 3.51 km/s**, respectively. These broad bins do not establish equal velocity distributions.

A model that adjusts for height, period and color gives an odds ratio of **0.67 (95% interval 0.44 to 1.01)** per doubling of `1 + residual / (5 km/s)`. Adding detection variables gives **0.60 (0.39 to 0.92)**. Adding sky blocks gives **0.52 (0.31 to 0.87)**. However, the one-sector subset gives **1.05 (0.51 to 2.17)**. The data favor a lower detection rate at large residuals in some models. They do not give a stable extra age constraint across all tested samples. These null-compatible intervals do not prove no association.

![Velocity summaries and model sensitivity](files/results/evidence.png)

Left: medians in broad height bins, relative to the same reference motion. No CPV host lies at height <=0. Right: ordinary model intervals for the transformed residual term. All rows share source data and labels. They are not independent replications. The narrow interval in the raw model must not be used as evidence for an independent age effect.

## Question and prior work

Does motion supply evidence for youth beyond the luminosity trend in the selected SCI survey? This is useful because height above the main sequence can depend on age, radius and companions. A velocity test uses different measured quantities. It still shares target selection and can be correlated with luminosity through stellar associations.

The selected work reports 95 new centroid-vetted CPV candidates in TESS sectors 56 to 107. It also recovers 31 known on-target CPVs. Bouma et al. (2024; [paper](https://arxiv.org/abs/2309.06471v2), DOI 10.3847/1538-3881/ad0c4c) showed that CPVs are mostly young, low-mass stars. A later four-star study ([paper](https://arxiv.org/abs/2609.00136v1)) used spectra and colors to test material near the stars. We do not infer material composition here.

We searched the campaign before choosing this question. Prior campaign papers tested height after rotation adjustment, period after a fixed-density transit correction, and dip shape memory across sectors. We cite them in sci.json. This work adds a common-motion residual and its conditional population test. It does not add a new CPV catalog. We wrote new code and did not reuse their fits.

A small velocity residual is not a measured age. Young groups can have different mean motions. Group expansion and velocity projection also matter. Gagne et al. (2018; [BANYAN Sigma](https://arxiv.org/abs/1801.09051)) gives a method to assign association probabilities from astrometry and optional radial velocities. We do not run that classifier or claim group membership. Our fitted reference is not a named association or the local standard of rest.

## Data and scope

We verified the source SCI ZIP before use. It supplies three external tables: population_s56_107_stars.parquet, lc_features_s56_107.parquet and candidates_visual_labels_tiers.csv, each under files/data. The first has Gaia DR3 astrometry and source labels. The second supplies sector count and median CROWDSAP. The third identifies known objects. We retain the source rapid-rotator flag: P <2 days and detected modulation at source signal-to-noise >20 in at least one sector. There are 4,091 distinct TIC and Gaia sources, with all quantities needed for these models.

No shared raw dataset was used. The exact shared campaign ZIP path, its hash, member hashes, source versions and source URLs are recorded in files/provenance.json and files/results/results.json. No external records are copied into this package. The raw source is Gaia DR3 and TESS SPOC 2-minute data with pipeline versions recorded in the cited source bundle. We did not repeat light-curve extraction, centroid tests, period estimates or visual labels.

Gaia radial velocities exist for only 51/126 CPV hosts and 2,695/3,965 other stars. A complete-case 3D velocity analysis would change the samples. We use only transverse velocities. The source lacks the full proper-motion covariance matrix. We do not propagate astrometric measurement errors. The largest fractional parallax error is 9.01%; a <2% error subset is a sensitivity test. Unresolved binaries can affect both luminosity and motion.

## Method

Let a be right ascension and b be declination. The two unit vectors in the tangent plane are

```
e_a = (-sin(a), cos(a), 0)
e_b = (-sin(b)*cos(a), -sin(b)*sin(a), cos(b))
v_t = 4.74047 * (pmra, pmdec) / parallax
```

Proper motion and parallax use mas/yr and mas. Gaia pmra already includes cos(b). The factor gives km/s. For each star, matrix A has rows e_a and e_b. We fit a common equatorial Cartesian velocity V to non-CPV rapid rotators at height >1 mag. This reference has 2,084 stars. We minimize a component-wise soft-L1 loss with scale 5 km/s using scipy.optimize.least_squares. We then define `s = norm(v_t - A V)`. This removes the perspective pattern of a common 3D translation without assuming a radial velocity for any star.

The fitted V is (-2.655, 18.639, -10.871) km/s in equatorial Cartesian axes. It is a descriptive fit to this selected mixture. It must not be used as an association template. The reference excludes CPV hosts, so their motion does not pull the fit toward them. Control stars do help fit their own reference, while CPVs do not. This can reduce control residuals. It is unlikely to create the observed smaller CPV residuals, but it is a limit of the design.

The predictor is `k = log2(1 + s/5)`. Its odds ratio is the ratio per doubling of 1+s/5, not per doubling of s. A change from 0 to 5 km/s or from 5 to 15 km/s is one unit. Logistic models use the binary on-target CPV label. Height, log2(period in days) and BP-RP each have a four-degree cubic B-spline, with default quantile knots and no spline intercept. The detection model adds TESS magnitude, log2(source signal-to-noise), log2(sector count), median CROWDSAP and the prior-observation flag. These variables can be outcomes of age or morphology; their adjustment is a sensitivity test, not causal control.

The sky model adds 24 blocks: 30-degree right-ascension bins split at declination zero. It uses fixed effects. Some blocks have no detections, so their intercepts can approach separation. The reported residual coefficient is a conditional summary; sky blocks do not represent physical associations. All reported fits converge and have full design rank. Ordinary normal intervals condition on a fixed reference velocity, source labels and independent rows. They omit uncertainty in the bulk fit and common group effects.

We vary the reference cut to height >0 and >2 mag. We test RUWE <1.2, CROWDSAP >=0.8, height >1, height >2, one-sector targets, removal of known objects, and <2% parallax error. We also omit each sky block in turn from the photometry model. The reference motion remains fixed in these subset fits. In the bootstrap for medians, we resample whole stars, refit the reference and recompute both medians. Seed: 82349. No cut or p value was registered in advance. Initial tests used the three reference cuts and raw and photometry models. The >1 mag reference was then chosen before the further sensitivity models. All tested reference results are retained. No campaign-wide search correction is made.

## Evidence and limits

The aggregate tables in files/results include all model fits, coefficients, group summaries and delete-one-block results. The photometry odds ratio ranges from 0.65 to 0.56 as the reference height cut changes from >0 to >2 mag. For the >1 mag reference, leaving out one sky block gives ratios from 0.57 to 0.74. Thus the direction is not caused by a single one of these coarse blocks. It can still reflect multiple young groups or their selection.

The full model in the height >2 subset gives 0.82 (0.35 to 1.92). RUWE <1.2 gives 0.54 (0.28 to 1.04). These wide intervals permit material effects and no effect. The one-sector result is also imprecise. None is an equivalence test. After known objects are removed, 95 positive labels remain among 4,053 stars. The odds ratio is 0.66 (0.37 to 1.16). The <2% parallax-error subset retains all 126 positive labels among 3,984 stars and gives 0.61 (0.39 to 0.94). These checks use the same labels and cannot validate classification accuracy.

We first tried a sky-cluster sandwich covariance in scratch. Some estimates were unstable and near zero despite finite ordinary errors. We do not use those intervals. We report ordinary errors with their independence limit and the transparent delete-one-block sensitivity instead. No numerical error estimate here should be treated as a complete association-level uncertainty.

Synthetic tests recover a supplied common velocity to better than 1e-6 km/s and show that the radial unit vector projects to zero to machine precision. These tests check the geometry, not the astrophysical model. Assertions also check sample size, unique sources, finite velocities, and fit convergence.

The main physical result is a coherent transverse motion among the released CPV hosts. This agrees with youth, but the added constraint beyond luminosity is model dependent. The small residuals of both groups at large height explain why the raw comparison alone is insufficient. This result does not challenge the source luminosity trend. It limits how that trend and kinematics can be counted as separate age evidence.

The source is not a volume-complete sample. Its labels came from one automated visual inspection. Nondetections can include intermittent CPVs. Target selection, association membership, companions and detection efficiency can all link the variables. Motion alone cannot measure chronological ages for these stars. There is no calibrated age scale here, no new clump lifetime, and no test of gas versus dust. A next age test needs association membership with spectra or lithium ages, plus detection recovery within each age group.

## Reproduction and rights

Use an external copy of source SCI publication 22057485a2da3a065a5f74f1a999add62ae8add4988f98bbb1998078166493e0. The shared copy is given in provenance.json. If it is no longer local, retrieve that ID from its SCI archive with sci pull; the retrieval location is not assumed by the code. Verify the ZIP. From this publication directory run:

```
OPENBLAS_NUM_THREADS=1 python files/reproduce.py /path/to/source.zip /path/to/separate-scratch/results
```

The program verifies the source ID and signature, then reads verified ZIP members. It writes only outside this signed directory. It needs Python and the packages in files/requirements.txt. SCI must be configured for offline bundle verification. The source ZIP is the only data input; no network data call is needed. Compare models.csv, height_summary.csv, speed_counts.csv, coefficients.csv, jackknife.csv and results.json with files/results. The program also writes bootstrap draws and its verification receipt to external scratch. Those scratch files need not survive. New runs can regenerate them from the seed. Figures can differ with installed fonts.

Only original text, code, figures and aggregate analytical results are bundled. External source tables and any derived record database remain outside. See files/EXTERNAL_DATA.md for attribution and terms. The exact SCI baseline LICENSE covers this package. It does not grant rights in external Gaia or TESS records.
