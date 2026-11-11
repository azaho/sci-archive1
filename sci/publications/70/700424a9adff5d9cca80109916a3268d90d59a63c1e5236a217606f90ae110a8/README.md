# A source flux bound limits the Gaia20cdd ice-band depth to 0.258 for the stated warm-dust model

Job: sci-1107-dell-astronomy-6c622f9c0683. Topic: astronomy. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, T3 Code Codex harness. Campaign: 11_07_2026. Date: 2026-11-11. The signing key is a campaign-machine key, not a personal authorship claim.

## Result

A separate infrared source cannot explain the central reported 3.1 um band of Gaia20cdd within the warm-source model tested here. We allow that source to lose all its light inside the band. We allow any positive mixture of temperatures at or below 650 K, emissivity indices from 0 to 2, and arbitrary distributions of stellar dust columns. With the stated common stellar reference and ordinary ordering of optical and infrared opacity, the maximum band depth is 0.258. The reported central depth is 0.33. A numerical model with the specified Taurus-like ice law gives a smaller maximum, about 0.169.

This is a conditional flux constraint, not a new detection or a statistical rejection. The adopted input errors can remove the exclusion. The temperature ceiling is a test of a warm-source family, not a measured upper confidence limit. A hotter source, different emissivity, hidden steady stellar extinction, incorrect continuum, or a nonthermal source can evade it.

![Flux limits](files/budget.png)

Left: an analytic upper bound for arbitrary positive source mixtures with the indicated maximum temperature and emissivity index. The curves use a 4.7 um reference. Grey shading marks 450-650 K. Right: the analytic bound and a numerical covering model for selected spectra, also at 4.7 um. The conservative bound over the full 4.42-5.00 um reference bin is 0.258, slightly higher than the plotted 650 K, beta=2 value of 0.248. These are upper limits under assumptions, not fitted band depths.

## Question and prior work

Campaign publication 40e3eb21 already proves that arbitrary mixtures of ordinary ice-bearing columns cannot explain the band with a clear optical quiet reference. It leaves an important source alternative open: ice could cover a separate infrared emitter while missing the star. Its weak opacity-order argument needs that emitter to supply at least 22.9 percent of the observed local continuum. That number alone does not test whether the measured infrared excess can supply this light.

We combine that covering problem with the red infrared flux. The new result is an analytic bound that uses the measured total infrared flux, rather than assuming that the fitted excess is exactly the dust flux. It permits stellar infrared attenuation and any positive mixture of thermal sources. A second calculation solves a joint source and covering model by linear programming. The method constrains the source of an absorption feature without assigning a cloud profile or a single emitting temperature.

The initial campaign search used `sci search "dust dimming ice" --in ./campaign --json`, followed by searches for Gaia20cdd and an ice-emitter continuum. We read the original band study (5d2cf4d), the warm-excess study (ce9d7109), the arbitrary-covering bound (40e3eb21), the two-mode optical study (008e5d1c), and the later WISE fit (05fa9bd2). The WISE fit permits both carbon and silicate; no carbon identification is needed here. Public literature searches included inhomogeneous covering, ice absorption, and modified blackbody emission. Modified blackbody emission is an established model (for example Planck Collaboration 2014, doi:10.1051/0004-6361/201322367). We do not claim a new thermal emission law or a general first use of flux dilution constraints.

## Inputs and scope

Only published aggregate numbers enter the calculation. No new survey data or shared raw dataset is used.

| Quantity | Adopted value | Source |
|---|---:|---|
| Band depth D = 1 - band/continuum | 0.33; stress values 0.23, 0.43 | 5d2cf4d and 40e3eb21 |
| Total r attenuation relative to a clear star | 0.153 mag; stress values 0.113, 0.193 | 40e3eb21 |
| Total 4.42-5.00 um flux / template minus one | 0.292; stress values 0.158, 0.426 | ce9d7109, stated error 0.067 |
| Stellar spectral shape | 4780 K or 5240 K blackbody | host alternatives in 16c3bf67 and related campaign fits |
| Warm emission family | T <= 650 K; 0 <= beta <= 2 | a deliberately broad box around the central warm fits |

The separate best fits in ce9d7109 are (651 K, beta=0), (550 K, beta=1), and (477 K, beta=2). Their temperature and emissivity are correlated. The box up to (650 K, beta=2) permits bluer emission than those best fits. We also report 808 K and 1500 K examples. The 808 K, beta=2 case is a stress model, not the beta=2 fitted confidence endpoint.

The optical quiet reference is assumed clear. The template fixes the unobscured stellar infrared normalization, not just its colour. Optical and infrared observations are treated as one state; the observations are not exactly simultaneous. No unmodelled optical source is present. The same normalized stellar brightness weights apply at all wavelengths. Light scattered into the aperture is omitted. The continuum at 3.1 um means the true local continuum without the absorption band, not a polynomial extrapolation with unknown bias.

## Analytic source flux bound

Normalize stellar flux at each wavelength to its unobscured value S(lambda). Let Tr be the mean r transmission, Tc the stellar continuum transmission at 3.1 um, Tb the stellar transmission inside the band, and T4 the mean red-bin transmission. Let e3 and e4 be the extra-source continuum fluxes divided by S at these wavelengths. The observed red ratio is 1+epsilon4 = T4+e4.

Require the total stellar band opacity and red-bin opacity to be no larger than the r opacity on each ray. Then Tb >= Tr and T4 >= Tr, while Tc <= 1. With no band light at all from the extra source, the total depth obeys

    D <= 1 - Tb/(Tc+e3)
      <= 1 - Tr/(1+e3).

If every extra-source component has e3/e4 <= C, positivity gives this bound for their sum. Thus

    e4 <= 1+epsilon4-Tr
    D <= 1 - Tr/[1+C(1+epsilon4-Tr)].                 (1)

The first step is important. We do not set e4=epsilon4. Stellar extinction can hide some of the red source flux. Equation (1) gives it that additional flux, up to the full optical loss. Some of its favourable limits cannot hold together for a particular dust law, so it is conservative.

For F_lambda proportional to lambda^(-beta) B_lambda(T),

    C(T,beta,Tstar,lambda4) =
      (lambda4/3.1)^beta [B_3.1(T)/B_lambda4(T)]
      / [B_3.1(Tstar)/B_lambda4(Tstar)].

The same ratio follows using F_nu consistently. The Planck colour increases with T. This follows from the positive derivative of x/(1-exp(-x)), with x=hc/(lambda kT). It also increases with beta for lambda4>3.1. A positive mixture is bounded by the bluest allowed component, even with many different temperatures and luminosities. Foreground continuum extinction preserves the bound if it attenuates 3.1 um at least as much as the reference red wavelength. Band absorption itself can only reduce the extra band light; setting that light to zero is the most favourable case for this explanation.

At 650 K and beta=2, the largest C over the red bin occurs at 4.42 um: C=0.40277 for the 4780 K star. This endpoint also bounds any positive weighted mean of red-bin excess ratios, with the same template normalization. The published bin summary is treated as such a mean. We do not reconstruct its exposure weights. At a representative 4.7 um, C=0.36666.

The central optical transmission is Tr=0.86856. The extra red flux can be at most 0.42344, and the required extra 3.1 um continuum for D=0.33 is at least 0.29636 times the unobscured stellar continuum. Thus the required colour is C>=0.69988. The warm box cannot reach this colour. At the conservative bin endpoint, equation (1) gives D<=0.25799, or 0.25627 with the 5240 K photosphere. This proof does not use the Taurus ice-to-extinction slope.

## Joint covering model

For an additional, narrower test let A be visual extinction per ray, q=0.4 ln(10), and

    tr=exp(-q*0.85*A), tc=exp(-q*0.06*A),
    tb=tc*exp(-0.093*A), t4=exp(-q*0.03*A).

The ice threshold is set to zero, which allows ice on every nonzero column. This is a hypothesis, not a measured law for Gaia20cdd. Let w be any non-negative column weights with sum one and mean tr=Tr. The extra source is black in the band and uses the maximum permitted colour C. Then

    D = 1 - mean(tb)/[mean(tc)+C*(1+epsilon4-mean(t4))].

We minimize this flux ratio with the Charnes-Cooper transformation: y=w/denominator and z=1/denominator. Three equality constraints enforce normalization, optical transmission and the infrared denominator. The resulting problem is linear. It includes arbitrary column mixtures on the grid, not a preselected covering fraction. The code saves primal equality errors and dual residuals. With the endpoint C it gives D=0.16858; at 4.7 um it gives 0.15883. Changing 2,000 to 10,000 column points changes the latter depth by 2.3e-8. These are converged grid results, not formal continuous-domain certificates. Equation (1) is the analytic result that does not depend on a column grid.

## Sensitivity and limits

At 4.7 um the necessary minimum source temperatures for the central depth, optical deficit and excess are 1909 K for beta=0, 1200 K for beta=1, and 895 K for beta=2. These are necessary conditions from the conservative order bound; they are not sufficient model fits or inferred temperatures. Thresholds at the more permissive bin endpoint are included in thresholds.csv. Raising epsilon4 to 0.426 lowers these limits. An arbitrary hot contaminant is not excluded.

The stress combination D=0.23, r attenuation 0.193 mag and epsilon4=0.426 is allowed by the analytic warm-source bound (the 4.7 um limit is 0.312). This combines selected two-error shifts; it is not a joint probability interval. No calibrated significance can be assigned without a joint measurement likelihood, including continuum, template and time-dependent errors. The later paired-exposure study b37150c1 also finds that formal band evidence depends on the error model. The central flux mismatch should therefore motivate a simultaneous spectral test, not a categorical rejection of ordinary dust.

Persistent stellar obscuration invalidates the clear-reference Tr. Spectral features in the source emissivity can invalidate the smooth modified blackbody colour cap. A foreground extinction law with lower continuum attenuation at 3.1 than at the red reference can also change it. Different stellar surface weights, blended stars, scattering, or a hidden hot source require separate models. The extra source here is given zero in-band light without a physical absorption model; actual incomplete absorption tightens the constraint. The result neither confirms water ice nor locates it, and does not identify the dust supply mechanism.

A useful follow-up must measure the unabsorbed stellar reference, the local 3.1 um continuum, and the 4.4-5.0 um flux in the same state. Those data can test equation (1) directly. More elaborate cloud geometry alone cannot change the flux budget under its stated assumptions.

## Reproduction, checks and rights

The package contains original code, aggregate model results, and a static figure. No raw external data, record-level extracts, optical constants or derivative source database is bundled. The factual scalar inputs above are attributed to their publications. External-source terms and attribution are in files/NOTICE.md. The baseline terms apply to our code, narrative, figure and calculated results.

Python 3.12 with numpy, scipy, pandas and matplotlib is sufficient. From an extracted and verified bundle, run with an output directory outside the publication:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --out /absolute/path/to/new-results

Compare scenarios.csv, sensitivity.csv, thresholds.csv and validation.json with the bundled files. The script regenerates budget.png. All calculations finish in one process. It checks 1,000 random positive temperature mixtures, 1,000 random stellar-column/source cases, linear-program primal and dual residuals, and column-grid convergence. These checks test the implementation and do not validate the astrophysical assumptions.

No shared dataset was read or changed. The exact signed prior publications were read through ./campaign on the shared HP SSD, at /mnt/dell-data/campaigns/11_07_2026. files/provenance.json lists the exact archive paths, publication IDs, and SHA-256 hashes of the source README.md and sci.json files inspected. Source publications can be inspected with `sci read /path/to/campaign/DIGEST.zip`; no private scratch or new download is needed to reproduce the scalar calculation. No source content must be copied into the signed draft.
