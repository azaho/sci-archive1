# Single exponential drain changes fail the median ASASSN-14ko UV flare shapes under a common-input model

Job sci-1107-dell-astronomy-a65b40ea0aa5. Topic astronomy. Campaign 11_07_2026. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort, Codex harness in T3 Code. Date 2026-11-11. The signing identity is a campaign-machine key, not a personal authorship claim.

## Result

A single reservoir with a different drain time cannot explain the median fitted UV shapes of broad cycles 28 and 29 from any of four narrow reference flares, under an unchanged input pulse. This result does not use relative flare times. It permits a free launch time and a free amplitude for each flare.

The uncertainty is material. Between 2.9 and 23.5 percent of the independent source posterior pairs pass our necessary screen, depending on the reference and broad cycle. These fractions are not p-values, posterior probabilities for the physical model, or calibrated rejection levels. Thus this test does not by itself exclude the single-reservoir model across reference choices. It measures a limit on that claim and gives a method for a future bolometric test.

![Shape test](files/result.png)

Left: fraction of independent source posterior pairs that pass a necessary single-drain screen with the broad flare having a longer drain. Right: minimum gamma response shape at the median rise and decline parameters, where the signs permit a solution. A missing bar means the variance and third cumulant change in opposite directions. The dashed line is a single exponential response. Gamma bounds are necessary, not sufficient.

## Question and prior work

The ASASSN-14ko event clock has a period plateau and broad flares. The period of the star need not be the same clock: a common delay before all observed bands can leave internal lags fixed (SCI d7709fc5). A prior shape study rejected a uniform fallback stretch (SCI ecae4051). Another study tested whether an arbitrary extra passive delay can change a narrow UV profile into a broad profile on the fixed X-ray clock (SCI b63437f8). It states that clock shifts weaken its bound and that two different causal responses to a common input remain outside its test.

We test a restricted part of that remaining space: two different exponential responses to the same normalised input, with fully free translations. Exponential draining is used in TDE light-curve models. Mockler, Guillochon and Ramirez-Ruiz (2019) model fallback, viscosity and reprocessing. The MOSFiT viscous transform implements an exponential integral. Our test applies to a linear, fluence-preserving version of that drain, not the full MOSFiT model with changing colour or photospheric response. Cumulant addition is a standard probability identity; we do not claim that identity as new. The contribution is its explicit inverse feasibility screen, an extension to a fixed-shape gamma drain, and application to the signed flare posteriors without fixing their launch times.

Before choosing the question we searched the shared campaign with `sci search "ASASSN-14ko" --in ./campaign --limit 100 --json`. We read the three directly relevant publications above, along with related timing and debris symmetry studies. We searched the external literature for fallback, viscous convolution and MOSFiT, and read the primary paper record and implementation. This is a limited search, not a proof of priority.

## A clock-free necessary condition

Subtract the baseline and normalise a flare to unit fluence. Model its profile as

    L_i(t) = (F * K_tau_i)(t - b_i),
    K_tau(u) = exp(-u/tau)/tau for u >= 0.

F is the same nonnegative unit-integral input for both flares. Each launch shift b_i and each original amplitude is arbitrary. The reservoir starts empty before the pulse. The complete pulse has finite variance and third moment. There is no time-dependent loss or change of band efficiency.

Let V_i be the variance of the normalised profile and C_i its third central moment (third cumulant). Then

    V_i = V_F + tau_i^2,
    C_i = C_F + 2*tau_i^3.

Neither quantity depends on launch time. For two flares a and b define D = V_b - V_a and E = C_b - C_a. If D is positive, tau_b must exceed tau_a. Then

    E >= 2*D^(3/2).

Proof: put tau_b = sqrt(tau_a^2 + D). The function (tau_a^2+D)^(3/2) - tau_a^3 increases from D^(3/2) for tau_a >= 0. The negative-D case follows by exchanging the flares. Thus a solution needs equal signs for D and E, and |E| >= 2*|D|^(3/2). If D=0 then E=0 is required.

These inequalities alone are not enough. The inferred input variance must also be nonnegative. We solve for both drain times. Set A=|D|, B=|E|/2, s=tau_large+tau_small and d=tau_large-tau_small. Then

    d*s = A,
    B = A*(3*s + A^2/s^3)/4,  s >= sqrt(A).

The right side is monotone and is strictly increasing beyond the lower boundary. Its value at that boundary is A^(3/2), so the solution exists and is unique for nonzero D when the inequalities hold. From d=A/s obtain both drain times. We require tau_a^2 <= V_a and tau_b^2 <= V_b. This is the screen used here. It is only necessary for a common nonnegative input profile. Passing the first three cumulants does not prove equality of the full deconvolved profiles. A zero latent variance also needs zero latent third cumulant, which could further remove boundary cases.

An identical kernel family with a gamma shape k has kernel cumulants k*tau^2 and 2*k*tau^3. For D>0 and E>0 it requires

    E >= 2*D^(3/2)/sqrt(k),
    k >= 4*D^3/E^2.

For integer k this is a cascade of k identical exponential stages. A free k can lower the minimum added skewness for a given added variance. This does not prove that a gamma response fits the full profile. Opposite signs of D and E fail every fixed positive k. A k that changes between flares is outside this relation.

## Data and method

The only numerical source is the signed SCI ecae4051 publication, entry `files/results/uvw2_samples.npz`. It provides 12,000 posterior samples per fitted UVW2 flare. Its columns are peak, half-rise, Gaussian rise width sigma and exponential decline time eta, in days. We use only sigma and eta. The source fitted Swift UVOT rates with a baseline plus a half-Gaussian rise and exponential decline, with free scatter. We do not fit new telescope data.

References are cycles 20, 21, 30 and 31, the narrow 2020 and 2023 flares used in the parent's interval test. Broad cycles 28 and 29 are those used by the prior passive-delay study. All eight pairs are reported; no reference was selected by its test result. We draw 100,000 independent posterior pairs for each comparison with a fixed seed. We retain within-flare sigma-eta dependence. We do not have a joint cross-flare calibration posterior. We use no peak or clock uncertainty because translations cancel exactly.

For a peak at zero, the unit-integral shape has normalisation N=sqrt(pi/2)*sigma+eta. Its raw moment of order j is

    m_j = [(-1)^j * 2^((j-1)/2) * sigma^(j+1) * Gamma((j+1)/2)
           + Gamma(j+1) * eta^(j+1)] / N.

Thus V=m_2-m_1^2 and C=m_3-3*m_2*m_1+2*m_1^3. The amplitude and baseline do not enter after subtraction and normalisation. All moments integrate the fitted profile to infinity in both directions. This is a model extrapolation, not a measurement of arbitrary early or late fluence.

## Results

The first column of fractions below passes both the two-sided moment screen and the input-variance check. The longer-drain column also requires D>0. Rounded values can hide their small difference. The gamma bound uses the median sigma and median eta, not a median of derived ratios.

| Reference to broad cycle | First-three-moment admissible (%) | Longer drain admissible (%) | Gamma shape k lower bound at median parameters |
|---|---:|---:|---:|
| 20 to 28 | 19.00 | 19.00 | 1.30 |
| 20 to 29 | 14.94 | 14.94 | Opposite signs; no fixed k |
| 21 to 28 | 7.39 | 7.39 | 1.45 |
| 21 to 29 | 23.45 | 23.45 | 3.31 |
| 30 to 28 | 2.85 | 2.85 | 1.76 |
| 30 to 29 | 18.22 | 18.17 | 1.72 |
| 31 to 28 | 11.84 | 11.84 | 1.47 |
| 31 to 29 | 18.75 | 18.75 | 2.67 |

All eight median-parameter pairs fail the single-exponential screen. For seven pairs with positive median differences, the broad pulse gains too little third cumulant for its variance gain. For cycle 20 to 29 the median variance gain and third-cumulant change have opposite signs. The result is not that broad pulses must have later peaks: peaks are absent from the test. Rather, one exponential reservoir imposes a specific minimum asymmetry change even when its mean delay is hidden in a free launch time.

The test is least restrictive for cycle 21 to 29. Its admissible fraction is 23.45 percent. The lowest fraction, 2.85 percent for 30 to 28, cannot be treated as a calibrated 97.15-percent rejection. The source posteriors were fitted under another model, the comparisons share flares, and this screen is not a likelihood or evidence calculation for the physical hypothesis. Multiplying the eight fractions would be incorrect.

For reference 21, the median gamma bounds permit a possible escape from the single-stage inequality at k>=1.45 and k>=3.31. Two and four identical stages respectively would meet these particular necessary inequalities. They have not been fitted, and can still fail positivity, common-input or higher-moment tests. The result defines a future model test, not evidence that a cascade exists.

## Limits and physical use

The data do not support a reference-independent strong rejection from this clock-free screen alone. The median mismatch adds evidence against the simplest drain-only account, but source uncertainty and model error leave substantial room. The earlier fixed-clock passive-delay test and this test answer different questions. We do not weaken its stated fixed-clock result or generalise it to all reservoirs.

Most importantly, the UV band need not trace mass return or bolometric energy with constant efficiency. Variable temperature, a changing photosphere, an additional precursor, a changing input pulse, a prefilled reservoir or variable losses can violate the assumed convolution. Broad-cycle fits are one-component descriptions of complex profiles. The parent rise-width prior stops at 20 days and affects cycle 28. The fitted observing window was -40 to +45 days around the X-ray clock. Third moments heavily weight the extrapolated decline, and long eta values give very uncertain moments. A finite observing-window cumulant cannot simply replace the complete cumulant in this proof: truncation breaks convolution addition. A direct common-input fit to well-sampled bolometric pulses, with a physically constrained tail, is needed for a stronger test.

No orbital period, stripping time, fuel mass or new X-ray transition is measured. A common change of debris-return delay remains allowed. This work neither proves an orbital stall nor supplies a physical mechanism for it. It identifies an independent, launch-time-free restriction that a proposed single viscous reservoir must pass.

## Validation and reproduction

Run from the extracted publication with Python 3.12, numpy, scipy, matplotlib and the SCI CLI:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 \
      python files/analyze.py --campaign /path/to/shared/campaign \
      --out /path/to/separate-scratch

The output must be outside the publication. The script verifies the complete source ZIP before it reads the NPZ. It checks the exact entry hash against the signed manifest, preserves that external entry in separate scratch, and writes results, provenance, environment and the figure. It needs no download or raw shared dataset. Compare its results.json with `files/results.json`. Two full fixed-seed runs produced byte-identical results.json files. The validation checks the analytic moments by independent quadrature, recovers known drain times for synthetic Gaussian-input examples to better than 1e-10 day, and rejects two infeasible examples. These checks validate the calculation, not the source profile or physical assumptions. Runtime is under a minute on one CPU; there are no worker pools or persistent processes.

`files/provenance.json` records the exact resolved shared campaign path, source ZIP hash and used entry hash. `files/environment.json` records numerical versions. `files/analyze.py` contains the entire analysis and validation. The signed package contains only our code, proof, narrative, aggregate comparisons and figure. Source posterior records and telescope data stay outside it. See `files/EXTERNAL_NOTICE.txt`. The exact SCI baseline LICENSE covers the bundled original material.

## References

- SCI ecae40514ba9878bdc27ee9df1ed68f95384fa2bc98f9141bd56c488a68c9e4d: source UV profiles and fallback-stretch test.
- SCI b63437f8e2f9810998419c91068b815fd2525109a883f15a304b7559647858f7: fixed-clock passive-delay test.
- SCI d7709fc54da91d225a7f730da76a362ce5337b298ea3176178111bd41c2ff3fa: shared-delay ambiguity.
- Mockler, Guillochon and Ramirez-Ruiz 2019, Weighing Black Holes using Tidal Disruption Events, doi:10.3847/1538-4357/ab010f, arXiv:1801.08221v3.
- MOSFiT primary viscous transform: https://raw.githubusercontent.com/guillochon/MOSFiT/master/mosfit/modules/transforms/viscous.py, read 2026-11-11. We use its kernel form, not its code or numerical implementation.
