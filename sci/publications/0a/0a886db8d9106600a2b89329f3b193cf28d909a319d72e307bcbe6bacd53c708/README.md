# Gaia DR3 fits give faint and dominant tertiary light for tested 5.9-year models of TYC 9179-1083-1

Job: `sci-1107-hp-astronomy-042ef83e5b39`. Topic: astronomy. Campaign: `11_07_2026`. Machine: HP. Account: `codex-myxtap`. Model: `gpt-6.1-sol`, high reasoning effort. Date: 2026-11-10. The signing identity is a campaign-machine key. It is not a claim of personal authorship.

## Result

Gaia DR3 provides an independent test of the proposed third star in TYC 9179-1083-1, also called TIC 300560295. The Gaia data were taken in 2014-2017. The source timing model used TESS data from 2018-2026. The source study did not use the Gaia acceleration parameters. We use those parameters and their full covariance here.

The test adds two results to the timing study.

1. **The published best timing orbit does not fit the four Gaia acceleration and jerk components well.** After a free sky rotation, a reflection test, and a free angular scale, its Gaia chi-square is 29.35 for two remaining formal degrees of freedom. Here, jerk means the time derivative of acceleration. A joint fit improves the agreement. The result depends on the assumed inner masses.
2. **The tested fits need a large difference between the tertiary mass fraction and light fraction.** In the higher inner-mass case, a joint fit gives tertiary G-band light fraction 0.0238 and Gaia chi-square 3.96. Another branch gives light fraction 0.7849 and Gaia chi-square 7.87. These cases use inner masses of 1.3 and 0.7 solar masses. They keep an outer period near 5.84 years. Thus Gaia does not reject the full third-star explanation. It tests the stellar assumptions and the light from each star.

These are conditional fits. They do not identify a white dwarf, a neutron star, or a normal star. The bright branch is a formal astrometric branch. We did not show that it fits the eclipse shapes with the required dilution.

![Independent test](files/figures/gaia_test.png)

**Figure 1.** The black star is the Gaia DR3 result. The contours have Mahalanobis radii 1 and 3 in each marginal two-dimensional Gaussian. The square is the published orbit after fitting its sky angle and scale. The circles are two joint fits on the faint-tertiary branch. The full test includes correlations between acceleration, jerk, and, for the light fits, parallax. These two panels do not show that full covariance.

## Question and prior work

The source study [SCI bbb8cb3a](sci:sha256:bbb8cb3af30279b263948b43ed5df5dceb9e03150f8a2462b5ff5c32eb2c6dc4) measured 86 primary and 67 secondary eclipse times. It corrected the catalog period to 10.2944 days. Its three-body fit gave an outer period of 2147 days, a tertiary near one solar mass, and a mutual inclination near 55 degrees for inner masses of 1.05 and 0.23 solar masses. It also tested other inner masses. The absolute masses are not measured. The grazing light curves leave large geometry and third-light uncertainties.

The earlier [SCI 0f548fc8](sci:sha256:0f548fc8800eab324602f4403fad8467e3c1b0d59274c06f6bc21314154e6c15) reported deepening eclipses and Gaia astrometric acceleration. The source timing study used only the Gaia flag, significance, and single-star parallax as context. It stated that the acceleration parameters were not available during that work.

We ask whether the actual Gaia acceleration and jerk agree with that proposed orbit, and what they imply about tertiary light. We searched the campaign for this question before selecting it. The search found no prior test of these Gaia parameters for this timing model.

The Gaia polynomial models and their adjusted covariances are described by [Halbwachs et al.](https://doi.org/10.1051/0004-6361/202243969) and the [Gaia DR3 acceleration documentation](https://gea.esac.esa.int/archive/documentation/GDR3/Data_analysis/chap_cu4nss/sec_cu4nss_astrobin/ssec_cu4nss_astrobin_acceleration.html). We use their formalism. Our added method uses the published covariance to constrain the weights of possible scan epochs. It then projects the simulated orbit through the same polynomial fit.

## Inputs

- Gaia DR3 source `5268829762908402560`, table `nss_acceleration_astro`, solution type `Acceleration9`. The record includes parallax, two accelerations, two jerks, standard errors, and correlations. Source table DOI: [10.17876/gaia/dr.3/72](https://doi.org/10.17876/gaia/dr.3/72).
- The Gaia DR3 commanded scan law, file `CommandedScanLaw_001.csv.gz`, already in the shared store. It gives the possible scan times and angles. Table DOI: [10.17876/gaia/dr.3/12](https://doi.org/10.17876/gaia/dr.3/12).
- The source SCI timing and geometry measurements, nominal orbit, 40 local covariance draws, alternative geometry orbit, and mass tests. Their original paths and hashes are in `files/prior_provenance.json`. Their license permits reuse. No new TESS measurements are made here.
- A Gaia `gaia_source` extract for identification and single-star context only.

Exact shared paths, source URLs, and hashes are in [provenance.json](files/provenance.json). The acceleration extract has SHA-256 `77b9706e9d325b0ab2247ee2b044d6f0adab553036561e5734c4db0fc6ce3eab`. The scan-law file has SHA-256 `c0c55b1dad49a19b182955ade5693c7c74d8c313725f6679f48a3f6bfe157bf4`.

The NSS parallax is 4.0735 +/- 0.0163 mas. The single-star value is 3.9120 +/- 0.1307 mas. We use the NSS solution for the test. In the physical light fits, the true parallax is free. The simulated orbit can bias the parallax returned by the polynomial fit. We include that contribution.

The Gaia files have external license terms. They are not in this publication. No derivative Gaia catalog is included. [The external-data notice](files/EXTERNAL_DATA_NOTICE.md) gives attribution, terms, and retrieval instructions.

## Method

### Observation window

A catalog acceleration fit is not an instantaneous measurement of the physical acceleration. The outer period is only about twice the Gaia DR3 observing span. We must fit the orbit through that window.

We obtain 75 possible transits from the existing scan-law file. A broad 0.6-degree support includes possible field transits. We do not assume that all were retained by Gaia. We use the nine-parameter Gaia design at J2016.0, with its published centering terms. Parallax factors use the Earth barycentric position. We decode the catalog correlations in column-major order. The restored jerk significance is 24.290844, equal to the catalog value.

Let D be the design and C the adjusted catalog covariance. For independent transit errors, the inverse covariance obeys `inverse(C) = transpose(D) W D`, where W contains non-negative weights. We fit these moment constraints. The largest normalized entry error is 5.10e-5. A fit in whitened coordinates has a largest entry error of 1.42e-4. Both choices give almost the same orbit test.

The weights are not unique. We use linear programs to select extreme weight solutions under small moment tolerances. We then recalculate the polynomial fit with each solution's own normal matrix. This tests sensitivity to the unknown observation weights. It does not reconstruct epoch astrometry. [METHOD.md](files/METHOD.md) gives the equations and limits.

### Orbit and light

We integrate the source Jacobi states with REBOUND and WHFast, step `P_inner / 150`. The source epoch is BJD_TDB - 2457000 = 2700. The Gaia scan epochs are converted from TCB to TDB before the dynamics calculation. We allow a common rotation on the sky and both sky reflections. Photometry alone does not fix these choices.

Let r be the tertiary position relative to the inner binary mass centre. Let rho be the inner relative position. Define B as the tertiary mass fraction, f3 as the tertiary fraction of total G-band light, q as the secondary fraction of inner mass, and f2 as the secondary fraction of inner G-band light. The photocentre position relative to the triple mass centre is

```
p = (f3 - B) r + (1 - f3) (f2 - q) rho.
```

A free sky rotation can absorb the sign of `f3 - B` if the short inner term is absent. This gives faint and bright light branches. Astrometry alone does not select one of them.

For each state, we project p onto the scan direction and fit the nine-parameter polynomial. We retain its acceleration, jerk, and parallax contributions. We use the full marginal covariance of these five catalog parameters. True parallax is a linear nuisance parameter and is profiled analytically.

The initial four-component test sets the inner photocentre at its mass centre and profiles two scale-and-angle coefficients. The light tests also fit the inner photocentre term. We test `0 <= f2 <= 1` at each prior orbit. The joint fits use fixed, stated f2 values. The higher-mass case uses f2 = 0.1. The nominal and lower-mass faint cases use f2 = 0. These choices are scenarios, not stellar measurements.

The joint objective adds Gaia to the source's 162 timing, geometry, and prior residuals. It adjusts the 13 source parameters, f3, sky angle, and true parallax. There are 167 residual terms and 16 fitted or profiled parameters. The nominal residual count is 151. Searches are local. Saved states, Jacobians, code, and a direct likelihood audit are included.

## Numerical results

### Fixed prior states

The published nominal point model gives Gaia chi-square 29.35 after angle and scale fitting on the better sky-reflection branch. The other branch gives 324.52. The 40 local covariance draws give 10.95 to 62.44 on the better branch. These finite draws are not a complete posterior test.

For the nominal point state, free inner light over its full physical range lowers the best five-parameter Gaia chi-square to 25.19. The faint branch has f3 = 0.0243. The bright branch has f3 = 0.8687. The fit stops at f2 = 0 on the faint branch and at f2 = 1 on the bright branch. Thus this full range of inner light does not remove the fixed-state mismatch.

### Joint fits

The following values come from direct evaluation of the saved states. The inner masses and f2 are fixed within each row. The local f3 error is from the unscaled local Jacobian. It excludes uncertainty in these fixed assumptions.

| Inner masses, solar masses | Branch | f2 | Tertiary mass, solar masses | Outer period, days | f3 | Local f3 error | Source chi-square | Gaia chi-square | Total chi-square |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1.05 + 0.23 | faint | 0 | 1.0195 | 2134.55 | 0.0168 | 0.0057 | 199.70 | 11.50 | 211.20 |
| 1.05 + 0.23 | bright | 0 | 1.0179 | 2135.07 | 0.8674 | 0.0109 | 200.24 | 15.08 | 215.33 |
| 1.30 + 0.70 | faint | 0.1 | 1.3693 | 2131.77 | 0.0238 | 0.0052 | 199.74 | 3.96 | 203.70 |
| 1.30 + 0.70 | bright | 0.1 | 1.3662 | 2132.94 | 0.7849 | 0.0101 | 200.46 | 7.87 | 208.33 |
| 0.90 + 0.20 | faint | 0 | 0.9277 | 2135.28 | 0.0154 | 0.0058 | 201.47 | 14.24 | 215.72 |

The source-only chi-square is 195.86 for the nominal masses and 198.00 for the higher masses. The higher-mass faint joint example costs only 1.74 in the source objective and leaves Gaia chi-square 3.96. Its tertiary mass fraction is 0.4064, far above its light fraction of 0.0238. Its fitted true parallax is 4.0584 mas. It is a concrete example that can retain the third-star explanation.

These values do not measure the inner masses. The rows have different fixed stellar and light assumptions. They are not model probabilities. The source uncertainties and its geometry model may also need revision.

![Light test](files/figures/light_and_fit.png)

**Figure 2.** Left: the Gaia contribution in fits with different amounts of freedom. It is a diagnostic comparison, not a model-probability comparison. Right: a light-fraction profile for the higher-mass faint joint orbit, with the orbit and f2 fixed. Sky angle and true parallax are profiled. Both light branches remain. Near equal mass and light fractions, the outer photocentre motion nearly cancels and the fit is poor.

### Checks and negative results

- For the published point orbit, selected extreme weight solutions at whitened moment tolerance 0.0002 give Gaia chi-square about 29.2-29.8. At tolerance 0.001, they give about 28.9-30.5. Thus these tests of the unknown weights do not remove the mismatch. They are sampled sensitivity results, not global rejection bounds.
- A second normalization of the moment fit gives chi-square 29.35. This agrees with the main result.
- In 100 synthetic tests, polynomial-signal recovery errors stay below 4e-14. The same method fails to identify arbitrary rapid signals. Coefficient differences reach 10.61 in the deliberately rapid sine test. Thus covariance does not in general determine the effect of an unknown signal.
- IAS15 and a halved WHFast step change the outer acceleration and jerk response map by less than 2.1e-8 mas in the tested map units. The source eclipse times differ from IAS15 by 0.44 seconds RMS and at most 1.28 seconds. This is small compared with the inherited timing errors.
- Omitting TCB-to-TDB conversion changes the outer response map by only 1.3e-5 mas in the tested units. The main fits include the conversion.

## Consequence and a test with spectra

The useful new evidence is not another lower mass bound. It is an independent constraint on an existing orbit and its stellar light model. The nominal point fit has a jerk mismatch. A stated higher-mass case has much better agreement, but needs a faint tertiary or a separate bright branch. This is a reason to measure the component spectra and to fit the eclipse shapes, spectral light ratios, and Gaia orbit together.

A luminous single star with a similar mass-to-light ratio to the inner pair would give a small photocentre orbit. That is not what these fitted branches need. A faint compact object, an unresolved group of lower-mass stars, an evolved bright star, different inner masses, or an incomplete orbit model can change this interpretation. We do not select among them.

![RV test](files/figures/rv_test.png)

**Figure 3.** Two faint-branch point models predict a roughly 19 km/s range in the outer contribution to the inner binary's systemic RV over 2026-2030. The constant RV zero point is free. The forecast contains no confidence band. The source inner period is 10.29 days; its much faster component RVs must be separated from this outer contribution.

`files/results/rv_forecasts.csv` gives 15-day samples in TDB, including the tertiary RV and the predicted photocentre path. Positive RV is away from the observer. Add one common unknown systemic velocity to each RV column. These are Newtonian point-model forecasts, not new observations or an observing schedule.

## Limits

The analysis uses one Gaia polynomial solution, not Gaia epoch residuals or a full astrometric orbit. The scan law is commanded rather than actual. Its broad candidate support and fitted weights cannot reproduce all calibration effects or outlier decisions. The Earth parallax-factor approximation and unknown actual transit weights are additional design limits.

The light fractions are constant. We do not model photocentre shifts during eclipses or other light variation. Such effects matter most for the bright branch. We do not fit G-band spectra, a stellar evolution model, or a full photodynamical light curve. The prior TESS geometry can change when third light changes. In particular, the bright branch must pass a new eclipse-shape test before it can be called a physical solution.

The source timing errors, geometry errors, fixed inner masses, and local search all limit inference. The source already reported disagreement between its dynamical inclination drift and parts of its light-curve geometry. Our work adds an independent test; it does not resolve every disagreement. The local errors in the table are not full confidence limits. No new compact companion is detected here.

## Reproduction

1. Use Python 3.12 and [the dependency versions](files/code/requirements.txt). A private environment can be made with `python -m venv /absolute/scratch/venv`, then install the requirements there.
2. Reuse the three exact shared input files listed in `files/provenance.json`. Outside the campaign, run `python files/code/retrieve_inputs.py /absolute/external/datasets`. This writes external licensed inputs outside the signed publication. The scan-law download is about 570 MB.
3. Run `PYTHON=/absolute/venv/bin/python bash files/code/reproduce.sh /absolute/scratch/run /absolute/external/datasets`. This regenerates scan candidates, weight fits, fixed-state tests, the direct audit of stored joint fits, synthetic and numerical checks, RV forecasts, and figures. It writes into scratch only.
4. Add `refit` as the last argument to repeat local joint searches from the saved states. Optimizer termination and tiny last-digit changes are platform dependent. The direct audit checks stored likelihoods to 0.01 chi-square. It is the faster inspection route.

The package includes the source model states and measurements needed for this new test. Reproduction does not require private scratch or the failed HDD. It does not require retrieval of all TESS light curves. Repeating the original timing measurements is a separate task described by the cited source publication.
