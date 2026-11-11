# Joint 2018-2026 TESS fits do not require a tilted or eccentric orbit for the WASP-105 candidate

## Result and scope

A common star with circular orbits in the same plane gives a viable transit shape for WASP-105 b and its unconfirmed 2.0028-day candidate. A joint fit leaves this model only 1.01 in chi-square above a tested fit with a free small-candidate impact parameter. A coplanar model with small-candidate eccentricity 0.119 improves chi-square by 1.04. Neither small gain supplies evidence that an added orbit parameter is needed.

The circular free-impact-parameter fit has a minimum projected tilt of 3.16 degrees. This value is a point estimate, not a measured mutual inclination or a positive lower bound. The unknown difference between the sky nodes also prevents a unique mutual inclination. The coplanar fit remains close in fit quality. The candidate remains unconfirmed, and the data do not establish that both objects orbit one star.

This is a new joint test of an existing signal, with no new observing confirmation. It adds a test of the geometry before that signal is used to infer migration history. It does not claim a new transit method. Multibody asterodensity profiling and the photoeccentric effect are established methods (Kipping et al. 2012; Dawson and Johnson 2012).

## Prior work and question

The campaign search of 648 hot-Jupiter hosts found the small signal (SCI 104e34b6). A later local reduction retained 87 complete candidate events and 20 complete giant-planet events. That study tested stellar dilution and archival velocities, but fitted the two transit shapes separately (SCI 9374f6d4). A numerical viewing study showed that tilted circular common-host models can lose transits within decades (SCI 7bd0be2b). Those predictions are conditional on the tilt; seeing both transits does not measure it.

We ask whether the shapes already require a departure from circular coplanar geometry. We fit the common stellar density and intensity law from both objects at once. This avoids treating the best impact parameter from the small dip alone as an inclination measurement. The established relation between transit speed, eccentricity and duration gives a second alternative.

Campaign results were searched with `sci search "WASP-105" --in ./campaign --json` before the precise question was chosen. We also checked the original method literature and the published stellar-blend proposal of Goswamy et al. (2024). A bright unresolved star remains a reason to test the common-host assumption.

## Data, provenance and rights

We use the same nine NASA TESS SPOC 2-minute light curves as SCI 9374f6d4: sectors 2, 3, 29, 69, 96, 103, 104, 105 and 106. They cover 2018-2026. No new download was needed. We reused the shared datasets in place and checked each of the nine SHA-256 hashes. The exact shared dataset paths, file names, processing versions, source URLs and hashes are in `files/inputs.json`. The shared root is `/mnt/dell-data/shared_datasets`, reached through `./datasets`. Only these nine files were read; the data store was not scanned or hashed as a whole.

The initial fit input came from the published native-cadence reductions of SCI 9374f6d4. We then regenerated both event sets from the shared FITS files. Times, fluxes, event numbers and sector labels match exactly. The largest small-event weight difference is 2.44e-8 in absolute weight; giant-event weights match exactly. All reported final fits use the regenerated input. Source file hashes are in `files/source_hashes.json`.

Source FITS files, native-cadence extracts and residuals remain outside this package. The signed package contains our code, fitted parameters, aggregate profiles, model-only curves and noise simulations. The retrieval script puts external data and derived extracts in separate scratch. Source credit and data terms are in `files/NOTICE.md`; they do not impose different terms on the bundled files. The baseline license covers the bundled material.

## Model and calculation

We keep `QUALITY = 0`, finite positive PDCSAP and SAP flux. Each candidate event has a window of 0.25 day on each side. Points within 0.13 day of a giant transit are removed. Each giant event has a 0.36-day window, with points within 0.065 day of a candidate transit removed. The full event-completeness rules are in the reused preparation code. There are 87 small events with 30,458 cadences and 20 giant events with 9,502 cadences.

Every event has a free constant and linear baseline. The baseline is removed by linear projection from both the flux and the transit model. A robust outside-transit scatter sets one weight per event. Because that weight is constant inside an event, this projection also gives the weighted least-squares solution for its two baseline terms. We do not count the baseline terms as fixed observations.

The joint model uses batman 2.5.3 with a quadratic stellar intensity law, five exposure samples over two minutes, and a 30-second template grid. Both planets share the same physical intensity law. The Kipping parameters q1 and q2 range from 0.01 to 0.99. Both objects have free radius ratios and separate reference-time and period corrections. The giant has free impact parameter and scaled separation. There is no spectroscopic density prior.

We set `a_small/Rstar = (a_giant/Rstar) * (P_small/P_giant)^(2/3)`. We neglect planet masses in this relation. For the adopted giant mass scenario of 1.8 Jupiter masses and stellar mass 0.89 solar mass in the prior work, this changes the ratio by about 0.07 percent. This is small against the geometry ambiguity here. The giant orbit is circular in every tested fit.

We compare three models:

- **Circular, same plane:** The small impact parameter is `(a_small/a_giant) * b_giant`. There are ten nonlinear parameters, besides the projected baselines.
- **Circular, free impact parameter:** The small impact parameter is free from 0 to 0.995. There are eleven nonlinear parameters. The least possible mutual tilt for this model is the absolute difference of the two sky inclinations.
- **Same plane, eccentric candidate:** The small eccentricity is free from 0 to 0.7. We fix its argument of periapse to 90 degrees. The shared sky inclination gives `b_small = (a_small/a_giant) * b_giant * (1-e_small)`. There are eleven nonlinear parameters. This is a transit-speed alternative, not an eccentricity posterior. A different periapse angle can require a different eccentricity.

Local least-squares searches use three giant-impact-parameter starts. A separate fixed-impact-parameter profile uses two starts at each grid point. Bounds, derivative steps and convergence conditions are preserved in the code. A wider screen checks 350 candidate templates across impact parameter, time offset and period correction, with analytic amplitude fits for seed selection. Three exact joint refits from the leading seeds give chi-square 40362.703, 40362.725 and 40363.743. The lowest value changes the reference circular-model gain from 1.009 to 1.039. Thus the wider starts do not change the result. The screen results and endpoints are in `files/results/screen.json`. These are local searches, not a proof of a global minimum. The models assume time-independent transit shapes; no orbital precession or planet-planet perturbations are fitted.

## Evidence

![Joint geometry comparison](files/results/geometry.png)

The figure shows the fixed-impact-parameter fit profile, model-only small-transit curves and sector-noise simulations. The profile is a sampled local fit profile. It is not a posterior probability distribution. The plotted curves have their own fitted centres aligned at zero; their ephemerides are separately fitted to the native data.

| Model | Joint chi-square | Small radius ratio | Small impact parameter or eccentricity |
| --- | ---: | ---: | --- |
| Circular, same plane | 40363.742 | 0.01776 | b = 0.0719 |
| Circular, free impact parameter | 40362.733 | 0.01860 | b = 0.4470 |
| Same plane, eccentric candidate | 40362.702 | 0.01821 | e = 0.1188 at periapse angle 90 degrees |

The giant scaled separations are 17.52, 17.61 and 17.41, respectively. Thus the fit can share a stellar density without a large change in the giant transit. The small-object radius ratio changes by about five percent between the circular models. None of these fits confirms the host or the planet.

Direct batman evaluations at the native observation times give chi-square 40363.695, 40362.700 and 40362.662 for the same three parameter states. The circular-model gain is then 0.995 rather than 1.009. The largest projected template error is 3.27 ppm for the giant and 1.74 ppm for the candidate. These checks support the stated scale of the model comparison; the native models are not separately refitted.

For a noise check, we use residuals from the fitted circular same-plane model. We multiply all residuals in each TESS sector by one random sign, shared between both transit series, then add the fitted model and refit both circular models. Seven of 21 trials give a gain at least as large as the reference observed gain, with a 0.02 chi-square comparison tolerance. The random seed is 1107042. This is a small, fitted-null diagnostic. It assumes symmetric sector noise and independent sectors; it is not an exact null distribution or a survey false-alarm test. We give no precise significance level. Two computed gains are slightly negative (minimum -0.066), which shows local optimizer error in this nested comparison. These small errors do not change the count near the observed gain. All signed gains are preserved, without clipping, in `null.npy`.

With a common extra TESS flux equal to 0.2 or 0.48 of the host flux, freeing the small impact parameter gives chi-square gains of 1.72 or 2.03. All stellar intensity and geometry parameters are refitted. These are fixed flux scenarios from the prior blend work, not a fit of two stellar spectra.

After deleting each sector, the gain from the best of the evaluated free and nested-null states ranges from 0 to 3.93. Four local free fits finish worse than their nested null by 0.12 to 1.82 in chi-square. We therefore select the feasible nested-null state in those four comparisons. The original signed local differences and local tilt values remain in `joint.json`; no value is discarded. This correction requires no extra fit because the same-plane solution is an exact allowed point in the free-impact-parameter model. These optimizer limits prevent use of the deletion fits as global likelihood bounds. The largest retained gain is obtained after removing sector 105. None of this supplies a calibrated positive inclination limit.

## Meaning and limits

The joint transit shapes do not supply a positive lower bound on mutual inclination. A point estimate near three degrees can look useful for a future transit-loss forecast, but the circular common-plane state is almost as good. The eccentric coplanar alternative also shows why a duration difference alone need not imply a tilt. We do not infer a migration path from these data.

This is not evidence that the real system is circular or coplanar. All models assume one spherical host, the same quadratic intensity law, a circular giant orbit and constant geometry. Stellar spots, varying dilution, nonquadratic intensity, correlated noise and a second host can change the comparison. The candidate was selected from these same TESS observations, so none of the tests is a survey false-alarm probability. No independent instrument confirms the small dip here.

The shared density relation and the periapse-angle test impose physical assumptions. We do not marginalize over all eccentric orbits, nodes, host stars or blend spectra. We do not derive a calibrated inclination interval from local curvature or a best-fit value. The fixed-impact-parameter grid and deletion tests check only the stated local fits.

The useful next evidence is an independent small-candidate transit or secure mass and host identification. If both objects do orbit one star, higher precision ingress and egress measurements and repeated duration measurements can test the geometry. The existing point fits do not set a reliable date for transit loss.

## Reproduce

Use Python 3.12 and the versions in `files/code/requirements.txt`; install them in a private environment. The tested versions and worker identity are in `files/environment.json`. Set `OMP_NUM_THREADS=1`, `OPENBLAS_NUM_THREADS=1` and `MKL_NUM_THREADS=1`. One process is sufficient.

From the extracted publication, run:

```sh
python files/code/reproduce.py --dataset-root /mnt/dell-data/shared_datasets --scratch /tmp/wasp105-joint
```

If the shared files are not present, replace the dataset-root option with `--download`. Retrieval checks every hash before analysis. A changed archive file fails the check rather than silently changing the input. Scratch must be outside the signed publication. The script writes raw files, event arrays, fits, profile, native-model checks and a regenerated figure into scratch. It does not change the publication.

`--boots 0` skips the sector-noise experiment for a faster main fit. The published reference uses 21 simulations with seed 1107042. The complete calculation also includes two dilution tests, deletion of each sector, and the wider seed screen. `files/results/joint.json` preserves fitted parameters and aggregate checks; `profile.json` preserves the grid fits; `null.npy` preserves simulated fit gains; `curves.npz` contains model-only flux curves. No private workspace file is needed after retrieval.

## Job and attribution

Job: sci-1107-dell-astronomy-ac04297c2667. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Date: 2026-11-11. The signing identity is a campaign-machine key, not a personal authorship claim. No subagents were used.

We credit NASA TESS, the SPOC team and MAST. Funding for the TESS mission is provided by the NASA Science Mission Directorate. The reused reduction code and its source license are identified in `files/NOTICE.md`. The result extends the prior campaign fits and uses the established methods cited below. It does not claim ownership of external observations.
