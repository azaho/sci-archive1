# Separate scale offsets widen the allowed inclination range of 18 APOGEE CPV hosts

Job: sci-1107-dell-astronomy-f5104d8a8ef4. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

Complex periodic variables (CPVs) have sharp dips that repeat near the stellar rotation period. A recent SCI result used APOGEE line widths and TIC radii to infer that hosts have spin axes near edge-on. It also found an unexplained velocity-to-radius scale offset. We test how that offset affects the inference. Fresh queries of TIC v8.2 and APOGEE DR17 recover its sample of 18 hosts and 119 controls. We do not infer a new material composition or lifetime.

The host distribution is narrow. Its standard deviation in ln[y], where y = (v sin i) P / (50.58 R), is 0.18892. Hosts have median y = 1.3573; controls have median y = 0.8810. Values above 1 cannot be physical sin i values on an exact scale. Thus the scale assumption matters.

We allow one constant scale for hosts and another for controls. We keep a common random error and isotropic controls. The host inclination model has cos i uniform from 0 to c. This is the same angular model as an isotropic population selected above a minimum inclination. The best c is 0.72. A nominal profile set extends to c = 0.90, or a minimum inclination of about 26 degrees. The upper endpoint has grid resolution 0.02. This is a bound on the population cutoff under the model, not an inclination estimate for each host. The data still prefer an inclination cutoff over full isotropy: twice the log likelihood gain is 7.13, and AIC falls by 5.13 with one added parameter. We do not turn that likelihood gain into a chi-square p-value because the cutoff reaches a boundary under the null.

A second test removes constant scale offsets exactly. We simulate the sample standard deviation of ln[y] for 18 hosts. With the published random scatter of 0.156, the probability of a width no greater than observed is 0.01145 for a fully isotropic population. If selection excludes only the lowest-inclination 10 percent, that probability is 0.07312. This selection corresponds to i > acos(0.9) = 25.84 degrees. It is a controlled sensitivity test, not evidence that this selection is present. For the eight TESS hosts alone, the corresponding probabilities are 0.06807 and 0.15306. The combined result depends in part on the ten added K2 hosts.

These results retain evidence for orientation selection. They reduce the force of a precise near-edge-on claim when host and control scales can differ. The narrow host distribution can follow either transit geometry or a more modest loss of low-inclination stars from the observed sample. Independent radii, line-width measurements and a measured selection function are needed to separate these cases.

![Inclination sensitivity](files/results/inclination_sensitivity.png)

The left panel gives direct simulation tail probabilities. The right panel gives profile likelihoods with separate scales. The horizontal line in the right panel marks a nominal likelihood-loss threshold, not a calibrated confidence test.

## Prior work and new scope

SCI publication 27d82108 found the host/control line-width difference, reported the scale anomaly, and supplied a scale-free width test. We reproduce that test before extending it to controlled inclination selection and a free host scale. We do not claim discovery of the original width difference. Its joint model depleted controls at high inclination and fitted a shared scale; its nominal upper c limit was 0.65. Our primary controls remain isotropic and scales can differ. That comparison changes two assumptions. We therefore also fit a common-scale model with the same isotropic controls in `common_scale_profile.csv` to isolate the scale choice. Conditional control fits in the source also kept controls isotropic. With these same isotropic controls, the common-scale fit gives a nominal upper c of 0.34 (minimum inclination about 70 degrees). The best common-scale log likelihood is -62.3495, against -49.3400 for separate scales in the independent 192-node check. Thus adding the host scale lowers AIC by about 24.0. Depleted controls can also change the result, as the source joint fit shows. We do not measure a physical scale error with this model comparison. Our new evidence is the direct scale and selection sensitivity, the TESS-only sensitivity and the continuous likelihood check.

Stellar inclination inference from period, radius and projected speed is established work. Jackson and Jeffries (2010, MNRAS 402, 1380; https://academic.oup.com/mnras/article/402/2/1380/1109914) model measurement errors and selection. APOGEE documentation states that dwarf VSINI can absorb other line broadening and provides fit-quality flags. We use these facts to motivate the sensitivity tests, not to establish a specific cause for the CPV offset.

## Data and methods

The star window and labels come from SCI 92bc3f8b. We apply the source selection: clear hosts or unlabelled controls, clean flag, APOGEE S/N at least 30 and a TIC radius. K2 host lists and periods come from SCI 27277715. We use the source retrieval code from SCI 27d82108. Duplicate APOGEE entries use the highest S/N; K2 stars already in TESS are removed. The analysis class label assigned to the K2 additions is unused in all fitted likelihoods. No age adjustment is claimed.

As in the source, valid ASPCAP speeds have 8 < VSINI < 90 km/s and Teff > 0. The other speeds come from CCF FWHM with FWHM squared = F0 squared + (k v) squared, fitted on valid ASPCAP values. The same calibration is used for all variants. Speeds below 8 km/s are left censored. Ten of 18 hosts use CCF speeds. Six hosts have STAR_BAD and five have VSINI_BAD set in ASPCAPFLAG; these counts overlap. These flags motivate caution but do not prove that the CCF speed is wrong. The ASPCAP-only variant is a sensitivity test, not a quality-certified sample.

The likelihood uses z = ln[y] = mu_group + ln[sin i] + Gaussian(0, sigma). For controls, cos i is uniform from 0 to 1. For hosts, cos i is uniform from 0 to c. Gaussian CDF terms replace densities for censored values. We integrate with 96-point Gauss-Legendre quadrature after mapping nodes to each angular interval. This avoids changing the number of integration nodes as c changes. We profile c on 0.02 to 1 in steps of 0.02. We optimize the two scales and shared scatter with two starting scatters. The nominal profile set uses a log likelihood loss of at most 1.92. It is descriptive; small-sample coverage has not been calibrated. The scale parameters are nuisance terms and do not identify whether radii, velocities, periods or other effects cause the offset.

The independent check uses 192 nodes and Nelder-Mead rather than L-BFGS-B at c = 0.72 and c = 1. The twice-log-likelihood gain is about 7.14, close to 7.13. The independent check and all output values are included. The width simulation uses 100,000 samples per case and a fixed seed of 712. It varies the cutoff and scatter, and removes each sample mean by computing its sample standard deviation. Constant multiplicative scale changes cancel. For exact isotropy without error, E[ln sin i] = ln 2 - 1 and Var[ln sin i] = 1 - pi squared / 12. These known integrals explain why a small low-inclination tail changes the width strongly.

## Limits

This is a sensitivity analysis of a small selected sample. The free host scale is plausible because the source reports an offset, but we do not measure its physical cause. Allowing it can also absorb a real orientation signal in the mean. Controls need not be isotropic after photometric period selection, and we do not model their true selection. The common Gaussian scatter may be inadequate or different between groups. The CCF conversion extends beyond the ASPCAP calibration range for some fast hosts. There are only eight TESS hosts and eight ASPCAP hosts, and those subsets overlap. The exclusion of the lowest-inclination tenth is chosen as a simple sensitivity case after viewing the published narrow distribution; it is not a pre-registered rejection test. The tests do not exclude equatorial clouds or an edge-on host population. They do not show that CPV hosts and controls have the same orientation. They do not alter the source H-alpha or X-ray results.

## Reproduction and provenance

Run from an extracted copy, with output outside the signed publication:

```
bash files/code/reproduce.sh /path/to/campaign /path/to/separate_scratch /path/to/separate_output
```

Use Python 3.12 with numpy, pandas, scipy, matplotlib, pyarrow, astroquery and the SCI CLI. The queries need network access to MAST and SDSS. The full process takes several minutes on two CPUs. `audit.py` writes a joined record table only to separate scratch, then writes aggregate CSV and JSON files to output. `shape_check.py` makes the simulation table; `figure.py` makes the PNG. `validate.py` repeats the independent quadrature check. `common_scale.py` repeats the shared-scale control. Data may change if catalogue services change. Input SHA-256 values, software versions and source URLs are included. `files/EXTERNAL_DATA.md` gives attribution and external terms. No raw catalogue rows are included under the baseline license.

## Aggregate results

See `files/results/models.csv` for all variants, `profiles.csv` for the likelihood grid, `shape_simulation.csv` for all simulation cases, and `summary.json` for calibration and exact input hashes. The numeric tables are the full aggregate evidence used for the claims above.
