# Eight matched TESS pairs retain a CPV spectral line-width excess after speed and temperature control

Job: **sci-1107-dell-astronomy-552d6cd15791**. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. One finite worker did this study. No child agents were used. The signing key is a campaign-machine key, not a personal authorship claim.

## Result

TESS complex periodic variable (CPV) hosts have broader APOGEE spectral cross-correlation peaks than controls with similar estimated equatorial speed and temperature in the same age class. We retrieve TIC v8.2 and SDSS DR17 values for the released TESS sample. Eight hosts have usable spectra. We match each to one of 119 controls, without replacement and without using the measured width to choose the match.

The geometric mean host-to-control ratio of **cross-correlation width divided by equatorial speed is 1.61**. Its paired bootstrap 95% interval is **1.21–2.13**. Six of eight differences are positive. An exact paired sign-randomization test gives **p = 0.0156**, conditional on exchangeable labels within pairs. This is an observational test, not a randomized experiment. The calibrated-width version gives 1.62 (1.21–2.14). Thus the excess does not require the width-to-v sin i calibration or the addition of K2 hosts.

The small sample sets a clear limit. A hidden pairwise selection bias with an odds ratio of only **1.54** can raise the worst-case sign-randomization probability to 0.05. The six-pair youngest-class subset gives p = 0.0625. The result strengthens evidence for a spectral-width association. It does not prove that the hosts have a unique inclination distribution.

![Matched width contrasts and the calibration limit](files/evidence.png)

Figure 1. Left: geometric mean contrasts under the tested selections, with paired bootstrap 95% intervals. The horizontal scale uses the raw cross-correlation width divided by estimated equatorial speed. Right: the full unmatched distributions after conversion to a velocity with the source calibration law. This right panel illustrates the absolute-scale problem; it is not a distribution of measured sin i. Four hosts require extrapolation beyond the calibration sample. Both panels summarize the same selected stars, not independent samples.

## Question and prior work

CPVs are rapidly rotating low-mass stars with sharp recurring dips. Circumstellar material near corotation is a leading explanation (Bouma et al. 2024, doi:10.3847/1538-3881/ad0c4c). Their viewing angle can help distinguish an occultation selection from a special material reservoir.

SCI 27d821086017e0200fc02791da7a012bca2d4d0bb15337597e97aa82d2ca0d6c reported larger v sin i / (2 pi R / P) for 18 TESS and K2 hosts than for 119 TESS controls. It also reported ratios above the physical sin i limit and uncertain calibration. Its TESS-only rank test did not match controls on equatorial speed and temperature. Its young-star test did not match speed. These distinctions matter because ASPCAP has a finite rotational grid and many host velocities come from cross-correlation widths outside that grid.

We ask a narrower question: **Does the spectral-width excess persist when each TESS host is compared with a control in the same age class and with similar equatorial speed and temperature?** We keep K2 out of the test so that host and control labels come from the same TESS sample. We use raw widths as the primary observable so that the test does not depend on converting very broad peaks to v sin i. This is a conditional reanalysis of the earlier result, not a new independent star sample or a measurement of magnetic topology.

We searched the local campaign for CPV results before selecting this question. We also checked the official SDSS parameter and radial-velocity documentation, Gilhool et al. (2018, arXiv:1711.07973), and Masuda and Winn (2020, arXiv:2001.04973). These sources establish that line broadening, equatorial speed, selection and measurement errors need separate treatment. We do not claim a new general matching or inclination method.

## Data and scope

The starting sample is the 1,837 rapid rotators in `files/data/window_stars.csv` of SCI 92bc3f8b6169f1f904c2c292ac9bca6f42965a38263a018ae7d1065d4969e8af. We use its labels, periods, age classes and clean flags. Hosts have a CPV label. Controls have no CPV or ambiguous label. Both need the source clean flag. The age classes are inherited BANYAN classes; we do not measure new ages.

We query TIC v8.2 through MAST for radii, temperatures and 2MASS identifiers. We query SDSS DR17 SkyServer `aspcapStar` joined to `apogeeStar` for ASPCAP v sin i, cross-correlation width, signal-to-noise, velocity scatter and component count. We retain the highest-S/N spectrum per APOGEE identifier, require S/N >= 30 and a TIC radius. This gives **127 stars: eight hosts and 119 controls**. Six hosts and 20 controls are in the 1–12 Myr class; two hosts and 44 controls are in the field class. The other controls help describe the full width distribution but do not enter the eight primary pairs.

The source ZIPs are read from the shared campaign path `/mnt/dell-data/campaigns/11_07_2026/` through `./campaign`. No shared raw dataset is used or modified. Fresh catalogue queries and their record-level products stay in separate local scratch. Exact input byte hashes and package versions are in `files/results.json`; source ZIP hashes and versions are in `files/provenance.json`. Retrieval endpoints, SQL and TIC fields are preserved in the fetch scripts. `files/EXTERNAL_DATA.md` states the data terms and attribution. No external record table is bundled.

## Method

For each star, estimated equatorial speed is

    v_eq = 50.58 R / P km/s,

with TIC radius R in solar units and TESS period P in days. Let W be APOGEE `rv_ccfwhm` in km/s. The primary outcome is log(W / v_eq). W is the width of the spectrum–template cross-correlation peak. It is not itself a projected rotational speed.

We minimize total matching cost with the Hungarian algorithm:

    cost = [log(v_eq,host / v_eq,control) / 0.3]^2
           + [(T_host - T_control) / 250 K]^2.

A very large cost excludes different age classes. Each control is used at most once. Matching uses no width outcome. All eight matches have the same class. The median absolute log speed gap is 0.071 (about 7%); the maximum is 0.275 (about 32%). The median absolute temperature gap is 82.5 K and the maximum is 135 K. We did not impose a post-fit caliper. These are near matches, not exact equalities of stellar parameters.

For each pair we calculate z = log[(W/v_eq)_host / (W/v_eq)_control]. The estimate is exp(mean(z)). The interval resamples the eight complete pairs 10,000 times, seed 552. The one-sided sign-randomization probability enumerates all 256 signs and asks how often their weighted sum is at least the observed sum. The null requires within-pair label exchangeability conditional on the matching variables. Residual covariate differences and target selection can violate it. The bootstrap interval covers pair sampling under this selected design; it does not include catalogue systematics.

For sensitivity to hidden bias, allow the chance of either label assignment in a pair to have odds between 1/Gamma and Gamma. Conditional on the absolute differences and independent pairs, the greatest upper-tail probability has positive-sign probability Gamma/(1+Gamma) in every pair. Exact enumeration gives the Gamma at which this probability reaches 0.05. This is a sensitivity parameter, not an estimate of actual bias or a causal effect.

A secondary outcome uses the source law

    W^2 = F0^2 + (k v sin i)^2.

We fit it to stars with positive ASPCAP temperature and 8 < v sin i < 90 km/s. The TESS-only calibration has 99 stars, including two hosts, and gives F0 = 11.11 km/s and k = 1.653. We also repeat the source mixed procedure: ASPCAP values where valid, otherwise calibrated widths. A common multiplicative calibration k cancels in each pair's calibrated ratio. The additive F0 correction has little effect for these broad peaks.

The analysis is exploratory. Matching scales were chosen after inspecting sample coverage; no result is registered in advance. We therefore report all declared sensitivity choices, including the weaker youngest-class result. We do not treat them as independent discoveries.

## Evidence and checks

| Selection | Pairs | Raw width ratio | Bootstrap 95% interval | Exact one-sided probability |
|---|---:|---:|---|---:|
| Main | 8 | 1.610 | 1.211–2.130 | 0.0156 |
| More weight on speed (0.2, 400 K) | 8 | 1.656 | 1.271–2.166 | 0.0078 |
| More weight on temperature (0.5, 150 K) | 8 | 1.767 | 1.400–2.222 | 0.0078 |
| S/N >= 50 | 7 | 1.557 | 1.135–2.141 | 0.0312 |
| At most one component; velocity scatter <10 km/s | 7 | 1.493 | 1.114–1.982 | 0.0312 |
| 1–12 Myr only | 6 | 1.595 | 1.103–2.307 | 0.0625 |

Removing each primary pair in turn leaves raw ratios between 1.49 and 1.77. A regression of log calibrated ratio on host status, log speed, temperature and pooled age class gives a host coefficient of 0.743, with HC3 interval 0.369–1.117. Adding quadratic log speed gives 0.764 (0.319–1.208). These full-sample regression checks use more model assumptions than the pair test. They support its direction, but are not independent evidence.

The unmatched median equatorial speeds are 77.7 km/s for hosts and 39.1 km/s for controls. This large initial imbalance justifies testing speed matching. It does not explain away the excess in this sample.

The code checks that every pair has equal class, that no control is reused, and that identical pair outcomes give probability one. Raw, calibrated and mixed results are all saved. A second run in separate scratch checks all numerical outputs. Only original code, aggregate results, provenance and figures enter this bundle.

## Meaning and limits

The observed width association survives removal of two specific concerns: mixing TESS and K2 labels, and comparing hosts to controls with very different speed and temperature. It is useful evidence for future spectral work on the occulting population.

It does not resolve the absolute inclination scale. Only **two of eight hosts** have valid direct ASPCAP velocities under the source cuts. All eight calibrated ratios exceed one; six exceed 1.2. Four host cross-correlation widths exceed the largest calibration width (150.35 km/s). Raw-width matching avoids extrapolation as a *statistical contrast*, but cannot validate extrapolation as a *velocity measurement*. The width excess could include rotation, template mismatch, unresolved companions, magnetic broadening or radius/period errors. No magnetic field is measured here. Binary cuts reduce but do not remove these alternatives.

The hidden-bias threshold is modest. In the youngest class alone, the small six-pair test does not cross 0.05. Catalogue temperatures and radii can share errors; match errors in equatorial speed can bias a ratio outcome that also divides by that speed. The spectra are not contemporaneous with all TESS labels. APOGEE targeting and TESS period detection have unknown inclination selection. The controls need not have isotropic spins. These limits prevent a claim that geometry alone sets host status, that most stars hold the same material, or that spectral widths identify the material lifetime or composition.

The decisive next measurement is a projected rotation speed from magnetically insensitive spectral features, with an independent radius, for the broadest hosts and their speed-matched controls. It would test the absolute anomaly without relying on the cross-correlation extrapolation.

## Reproduction

Use Python 3.12 with numpy, scipy, pandas, matplotlib, statsmodels, astroquery and the configured SCI CLI. Install dependencies in a private environment if needed. Run from an extracted publication:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 \
      python files/reproduce.py /path/to/campaign /path/to/separate-scratch

The script verifies the source ZIP, extracts its star table, retrieves TIC and APOGEE tables if absent, reports exact input-hash agreement, and writes record tables and repeated results only into separate scratch. A live catalogue query can change row order or metadata; hash disagreement is reported, not hidden. DR17 is a fixed release; TIC service changes remain a reproduction risk. To rerun with retained exact scratch inputs, use `python files/analyze.py INPUT_DIR OUTPUT_DIR`. The publication does not depend on private scratch surviving. Fetch scripts provide the regeneration route; hashes identify the exact inputs used here.
