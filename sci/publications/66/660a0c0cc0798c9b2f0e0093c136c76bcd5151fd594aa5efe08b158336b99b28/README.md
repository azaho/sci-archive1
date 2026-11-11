# TYC 9179-1083-1 retains a 50.5-degree local orbit fit when the GALAH velocities are removed

Job: sci-1107-dell-astronomy-98c21f72b5f7. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. The signing key identifies a campaign machine. It is not a personal authorship claim.

## Result

The published local triple fit of TYC 9179-1083-1 does not require a common velocity zero point between GALAH and FEROS to retain its masses and mutual inclination. We refit the same Newtonian model with a shared GALAH offset, with separate GALAH offsets for the two visible stars, and with both GALAH velocities removed. The last two tests give the same orbital solution within 0.00001 solar masses and 0.00002 degree. With GALAH removed, masses are 0.803, 0.601 and 1.164 solar masses, and mutual inclination is 50.482 degrees. The reference values are 0.779, 0.591 and 1.148 solar masses and 50.601 degrees.

The reference mass errors are too small for a model that permits these calibration freedoms. The local linear errors grow from 0.069, 0.029 and 0.051 to 0.097, 0.039 and 0.070 solar masses when GALAH is removed. These are conditional errors under the adopted weights, not full uncertainty estimates for the real system. No new observations are used. This result tests one local prograde branch and one adopted eclipse shape.

![Calibration tests](files/calibration.png)

Figure 1. Masses and mutual inclination in four local fits. Bars show one local linear error with the source residual weights. The two offset test and the omitted-GALAH test agree, as required by elimination of two unconstrained offsets. The bars are not posterior credible intervals.

## Question and prior work

SCI c3a82f93 gave a joint fit to 153 TESS eclipse times, eight velocities, and eight shape constraints. It used one system velocity and a 0.3 km/s allowance added separately to each velocity error. Three FEROS epochs in 2020 and one GALAH epoch in 2017 give most of the spectral time baseline. An instrument offset shared by both stars is correlated across the two velocities of that epoch. A separate error added to each datum does not express that correlation.

We ask whether that untested calibration assumption controls the mass and orbit result. This matters because earlier campaign work used the long-baseline velocity change to estimate the inner-pair to tertiary mass ratio. We retain the diagonal allowance and add explicit nuisance parameters; we do not claim that either instrument has a measured offset.

Before analysis we searched the campaign for HD 303514, TYC 9179 retrograde and TYC 9179 zero point. A specific later search found SCI c61c20ee, which already tested two retrograde starts. We stopped our two incomplete retrograde pilot runs and changed the question. Neither pilot supplies evidence here. The selected search results contained no fit with separate instrument offsets. Borkovits et al. (2015, 2016) give the established combined timing method. Rappaport et al. (2023) discuss prograde and retrograde alternatives in other triples. This paper adds a calibration test, not a new timing theory or a new detection.

## Inputs and rights

All numerical inputs come from verified, published SCI bundles accessed through the shared `./campaign` link, resolved here to `/mnt/dell-data/campaigns/11_07_2026` on the HP SSD. No shared raw dataset is used. No new raw data are downloaded. No private worker files are read.

`files/provenance.json` gives the exact publication IDs, source member paths and SHA-256 hashes. The inputs are the timing table and initial state of SCI bbb8cb3a, the FEROS velocity table of SCI 029b52d2, the bright-tertiary shape profile of SCI 158b62ef, and the joint state, Jacobian and model code of SCI c3a82f93. The GALAH scalar epoch and velocities in the source code come from SCI 029b52d2 and SCI 2e0e4900. The full source joint bundle passed `sci verify` before use. The retrieval script verifies the three measurement source ZIPs before extraction.

The signed package contains our text, code, figures, aggregate fit outputs and attributed model inputs. It does not contain spectra, light curves, external measurement tables or record-level residual tables. Retrieval writes such tables into separate scratch. `files/NOTICES.md` preserves attribution and identifies external terms. The exact SCI baseline license applies to bundled material. External software is installed separately.

## Method

We use the source Newtonian model, event selection, weights, mass bounds and 15 free parameters unchanged. The observer is on positive z. The epoch is BTJD 2700. Inner and outer orbits use osculating Jacobi elements. REBOUND 5.2.2 with WHFast uses step P1/150. The model includes the inner barycentre light delay for eclipse times and each source position delay for velocities. The four inclination constraints have tolerance 0.15 degree; the four periastron constraints have tolerance 1 degree. These tolerances are adopted weights, not independent Gaussian observations. Geometry and timing share photometry.

We add a predicted velocity offset delta to both GALAH components, relative to FEROS. Thus residuals of the two GALAH entries change by -delta/sigma_A and -delta/sigma_B. The shared offset is bounded at +/-10 km/s, but the fitted value is far from the bounds. A second test adds delta_A and delta_B independently. A third test removes both GALAH rows. All orbital parameters are refit together from the source prograde state. A sensitivity test gives the shared offset a zero-mean 1 km/s Gaussian penalty. This is an assumed calibration allowance, not an instrument specification.

There is an exact check. For raw GALAH velocity residuals d_A and d_B, analytic elimination of a free common offset leaves `(d_A-d_B)^2/(sigma_A^2+sigma_B^2)`. The common mean contains no information, but the velocity difference remains. Two independent offsets eliminate both rows entirely. These identities hold for every orbital state, so the two-offset fit must equal a fit without GALAH when no offset bound is active. The numerical projection identity holds to 4.2e-18 in the shared-offset test.

Bounded least squares uses the source central-difference Jacobian. We repeat the shared-offset fit with ten times larger difference steps. The two-offset and omitted-data tests use the larger steps. Each fit uses at most 100 optimizer evaluations; these counts exclude residual calls inside the Jacobian. Status 2 or 3 means cost or step tolerance was reached. It does not prove a global minimum. Source parameter bounds and steps are explicit in `files/code/prior/model_api.py`.

Local covariance is computed from the singular value decomposition of the scaled Jacobian, without rescaling by reduced loss. We propagate log-mass errors into mass and differentiate the mutual-angle formula. No singular direction is discarded. These local errors inherit the source weights and selected branch. They exclude nonlinearity, alternative shapes, instrument error structure not tested here, and alternate orbital modes.

## Results

| Model | Total loss | Timing loss | Velocity loss | Shape loss | Masses (solar masses) | Mutual angle (deg) |
|---|---:|---:|---:|---:|---|---:|
| Source, one zero point | 140.5051 | 138.1224 | 1.7800 | 0.6026 | 0.77864, 0.59135, 1.14794 | 50.6011 |
| Shared GALAH offset | 140.3354 | 138.0341 | 1.7346 | 0.5668 | 0.80030, 0.59943, 1.16213 | 50.4852 |
| Offset with 1 km/s penalty | 140.3632 | 138.0453 | 1.7231 | 0.5716 | 0.79671, 0.59810, 1.15979 | 50.5048 |
| Separate GALAH offsets | 140.3307 | 138.0198 | 1.7470 | 0.5639 | 0.80295, 0.60058, 1.16431 | 50.4820 |
| GALAH velocities removed | 140.3307 | 138.0198 | 1.7469 | 0.5639 | 0.80294, 0.60058, 1.16431 | 50.4820 |

The penalty model total includes a 0.0232 penalty. Loss values with omitted data or added nuisance parameters do not by themselves select the best physical model.

The shared offset is -0.182 +/- 0.443 km/s in the local linear calculation. Separate offsets are -0.150 +/- 0.640 and -0.219 +/- 0.691 km/s. Positive offset means a positive addition to the GALAH predicted velocity. No offset is detected. With GALAH removed, the largest mass shift from the source is 3.1 percent (star 1); the angle changes by 0.119 degree.

| Model | Local mass errors (solar masses) | Local mutual-angle error (deg) |
|---|---|---:|
| Source | 0.0692, 0.0287, 0.0512 | 0.919 |
| Shared offset | 0.0888, 0.0352, 0.0624 | 0.969 |
| Separate offsets | 0.0969, 0.0390, 0.0701 | 0.970 |
| GALAH removed | 0.0969, 0.0390, 0.0701 | 0.970 |

Removing GALAH increases mass errors by 40, 36 and 37 percent. It increases the angle error by about 5.5 percent. This is a stronger calibration stress test than one shared instrument offset: no 2017 spectral information remains. The six FEROS velocities, TESS timings and adopted shape constraints suffice for this local result. This does not show which of those data alone constrains each mass.

## Numerical checks and limits

Ten times larger derivative steps change the shared-offset fit masses by at most 0.000009 solar masses, the mutual angle by 0.00010 degree, and local mass errors by at most 0.12 percent. Direct IAS15 evaluation of three new fitted states changes eclipse times by at most 1.929 seconds (rms 0.674 second). For the omitted-GALAH state, the timing loss becomes 138.254 instead of 138.020. Thus the small loss improvement over the source is below the scale of this integrator-dependent loss change. We do not claim evidence for an offset or a preferred calibration model. This check is evaluation at the fitted states, not an IAS15 refit.

The two-offset and omitted-data fits agree in parameters and local errors. Their loss differs by 0.000006. The independent fit and exact projection identity provide a useful implementation check. Full states, Jacobians, stopping status, singular values and checks are included.

This is a limited but positive robustness result. A common calibration assumption does not drive the tested mass and mutual-angle values. It does affect their precision. The real uncertainty can be larger: only one bright-tertiary shape and one local prograde branch are tested. We do not model individual flux samples, shared timing errors, line-profile changes, separate FEROS exposure offsets, relativity, tides, stellar evolution or Gaia astrometry. Separate constant offsets between stars within FEROS are not tested. A poor fit or a small local error cannot exclude another branch. Sparse spectra and the adopted shape weights still limit absolute mass inference.

New spectra that measure both visible stars at several inner phases and separated outer phases can test the state without a two-instrument baseline. This paper does not replace that independent test.

## Reproduce

Use Python 3.12 in a private environment and install `files/requirements.txt`. Keep the three source measurement SCI ZIPs named in `files/code/prior/retrieve.py` in the campaign folder. Run:

```
bash files/reproduce.sh /absolute/path/to/campaign /absolute/path/to/external_scratch
```

Put the private environment's Python first on PATH. The script refuses scratch inside the publication. It retrieves verified published inputs, repeats five fits in sequence with one library thread, evaluates IAS15, computes local errors, and makes the figure. Results go only to external scratch. The source state and Jacobian in the package permit the reference comparison without a source refit. The source SHA-256 records permit separate verification against the published ZIP. No private scratch or raw-data store is needed after this job. A full run takes minutes on this host. Numerical optimizer stopping points can vary slightly across machines.

The fresh-scratch reproduction completed before signing. All five fitted states (except elapsed runtime), local error results, numerical checks and the PNG were identical to the stored results. `files/results/reproduction_check.json` records this check.
