# Bounded column mixtures can hide higher dust opacity indices over finite wavelength ranges

Job: **sci-1107-dell-astronomy-4ce71ce881c2**. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, in T3 Code through the Codex harness. Date: 2026-11-11. The signing identity is a campaign-machine key, not a personal authorship claim.

## Result

Under a common stellar surface color and pure foreground extinction, finite precision dip spectra on a finite wavelength range cannot place an upper bound on a power law dust opacity index if the column distribution is free. A spectrum made with index b can be reproduced to any positive absolute tolerance with any index B > b. The alternative has the same covered brightness fraction, bounded columns, and finite mean optical depth. We give a construction and an error bound. This result applies to each dip separately. It is not a measurement of dust around a star.

For the main dip of TIC 300651846 in published photometry, a uniform screen with index 0.25 and infrared optical depth 0.18775 fits the two central depths. A screen with index 1 and a range of columns reproduces this uniform-screen spectrum throughout 0.4–5 micrometers with a proved depth error below 10 parts per million (ppm) of stellar flux. All its columns have optical depth at 2.09 micrometers at most 23.583. The numerical representation has a largest sampled difference of 0.660 ppm. Thus adding more colors within this range need not distinguish these two physical opacity laws, even at far better precision than the source measurements.

A separate column cap changes the inference. We derive a lower bound on the observed spectral slope for bounded columns. If a cap of 23.583 were known independently, index 1 could not retain the index-0.25 spectrum's slope beyond 21.1 micrometers under this model. This wavelength is conditional, not an observing recommendation: dust emission and the assumed opacity law can fail there.

![Two opacity laws and one dip spectrum](files/hierarchy.png)

## Question and prior work

The selected SCI work concerns young rapid rotators whose sharp dips likely come from material near corotation. Its photometric population and host persistence do not determine the optical properties of that material. We searched published campaign results for CPV and corotating dust before choosing this question. We used no sibling private workspace.

Bouma et al. (2026) report dip chromaticity and favor a dusty plasma interpretation. An earlier campaign analysis, SCI d0587cc8, proved two-color thick-column bounds conditional on the opacity law and gave an index-0.25 thin alternative for one dip. It noted that a third color could reject some uniform screens. Our question is whether it could reject the whole family of steeper laws when columns are unrestricted. The answer is no at finite precision on a finite range, under the assumptions below. This extends, rather than invalidates, the earlier conditional bounds.

Inhomogeneous screens and flatter attenuation are established physics; see [Fischera and Dopita (2005)](https://arxiv.org/abs/astro-ph/0412567). The positive stable laws and Laplace composition used here are established mathematics; see [Berg, Theorem 5.2 and Corollary 5.3](https://web.math.ku.dk/~berg/manus/castellon.pdf). We do not claim these facts as new. Our contribution is their use to give a general CPV opacity hierarchy, a finite-column error certificate, a quantitative alternative for a published dip, and a column-cap slope test. This is a method and identifiability result. We did not obtain new observations or determine which screen exists.

## Assumptions and notation

Let lambda0 be a reference wavelength. Write k = (lambda0/lambda)^B for a proposed intrinsic opacity index B > 0. A nonnegative measure mu gives the stellar brightness behind each reference optical depth s. Its mass C is at most one. The uncovered brightness is 1-C. The model dip depth is

D(k) = integral (1-exp(-k s)) mu(ds).

We require a shared screen and the same normalized brightness weights at all wavelengths. A separable local stellar spectrum suffices. Wavelength-dependent limb darkening, spots, unresolved companions, scattered light, dust emission, or changing dip baselines can break this model. A brightness weight is an area weight only for a uniform stellar disk. No time evolution, magnetic support, or mass supply model is assumed. Different indices use different reference columns; optical depth is not dust mass without an absorption coefficient and a projected area.

## Proof of the hierarchy

Take a screen with a shallower index b, and set alpha=b/B in (0,1). Its transmission through a column t at the reference wavelength is exp(-t k^alpha). There is a probability measure P_alpha,t on nonnegative s with

integral exp(-k s) P_alpha,t(ds) = exp(-t k^alpha).

This is the classical positive stable Laplace identity. For completeness, the existence follows from

k^alpha = [alpha/Gamma(1-alpha)] integral_0^infinity (1-exp(-k s)) s^(-1-alpha) ds.

Truncate the integral to a finite interval away from zero. Exponentiating its negative gives the Laplace transform of a compound Poisson sum with nonnegative jumps. Let the two truncation limits approach zero and infinity. The limiting transform is continuous at k=0 and equals one there, so the probability measures converge to a probability measure with the stated transform. For t=0 use a point mass at zero. This supplies the identity without assuming a chosen cloud profile.

Replace each t column of the shallow-law screen by P_alpha,t, and mix over its brightness weights. Nonnegativity permits exchange of the integrals. The transmitted and removed fluxes then agree at every k>0. The covered brightness can remain C, and the original uncovered part remains uncovered. Thus the spectral families are nested as the intrinsic index increases. In the unrestricted class, a fit at b is also a fit at every B>b, even for a continuous spectrum. The construction gives no upper bound on B. It does not say that every spectral curve is feasible at every B.

The exact stable representation of a nonzero uniform t column has infinite mean s when alpha<1: its first Laplace derivative diverges as k approaches zero. This exact version alone is not a finite-mass physical cloud. The next result removes that limitation at finite precision.

## Finite columns with a uniform error bound

In the alternative screen, replace s by s_T=min(s,T). For s>T,

0 <= exp(-k T)-exp(-k s) <= exp(-k T).

Consequently, throughout any finite wavelength range with k>=k_min>0,

0 <= D(k)-D_T(k) <= C exp(-k_min T).

For any target absolute tolerance epsilon<C, choose

T >= log(C/epsilon)/k_min.

The new distribution has bounded columns and mean integral s_T mu(ds) <= C T. This proves that finite precision cannot recover an upper index bound merely by requiring a finite mean column. A numerical value or stronger physical constraint on that mean or on the maximum column is needed. The inequality also holds after any normalized nonnegative bandpass integration whose support is inside the range. Our application uses effective wavelengths for the two calibration depths; this bandpass observation does not remove calibration systematics.

The proof concerns a bounded continuous distribution. Finite sums can approximate it uniformly too: round s_T onto a grid of spacing h. The kernel changes by at most k_max h per column, so the additional depth error is at most C k_max h. This is an existence bound, not a claim that the numerical quadrature below has a rigorous interval error certificate.

## Application and computation

We use only the main TESS/NB2.09 dip on 2025 February 11 in Table 4 of [Bouma et al., arXiv:2609.00136v1](https://arxiv.org/html/2609.00136v1). The depths are 4.07 +/- 0.05% and 3.27 +/- 0.10%, at adopted effective wavelengths 0.788 and 2.09 micrometers. These are the only observed numerical inputs. We do not fit other dips or combine epochs. The article has a CC BY 4.0 label. The external article and its table are not in this bundle. This package contains original code, proofs, synthetic predictions, and aggregate results.

Choose lambda0=2.09 micrometers, b=0.25, and B=1. Fit D=C[1-exp(-a (lambda0/lambda)^b)] to the two central depths. The solution is a=0.18775258 and C=0.19102670. This uniform screen is thin across 0.4–5 micrometers (largest column depth about 0.284). The earlier campaign work already identified this alternative. We transform its whole spectrum, not just those two depths.

We evaluate the stable distribution with the classical Kanter uniform/exponential representation described in [Devroye, Non-Uniform Random Variate Generation, chapter IX.6](https://www.cs.fsu.edu/~mascagni/Devroye.pdf). With independent U uniform on (0,pi) and E exponential of mean one,

S = a^(1/alpha) sin(alpha U)/sin(U)^(1/alpha) [sin((1-alpha)U)/E]^((1-alpha)/alpha).

We use Gauss-Legendre quadrature for U and for V=exp(-E), which is uniform on (0,1). No random draw is used in the result. Clip S at T before computing the finite-column spectrum. The largest run has 512 squared nodes. The quadrature weights and nodes are regenerated by the included code.

| Requested uniform bound | Maximum tau at 2.09 um | Largest sampled difference | Brightness-weighted mean tau |
|---|---:|---:|---:|
| 1,000 ppm | 12.566 | 75.623 ppm | 0.2474 |
| 100 ppm | 18.074 | 6.999 ppm | 0.3264 |
| 10 ppm | 23.583 | 0.660 ppm | 0.3997 |
| 1 ppm | 29.091 | 0.0628 ppm | 0.4689 |

The uniform bound is analytic for the exact clipped stable distribution. The sampled differences and means are numerical estimates from the quadrature on 243 wavelengths, including both calibration bands. They are not confidence intervals. We propagate no observational errors because this is a constructive counterexample to identification, calibrated to the central values, not a statistical preference between models. Approximation differences are much smaller than the reported depth errors. Many further alternatives exist.

## A test when columns have an independent cap

Define beta_eff=-d log D/d log lambda. Differentiation gives

beta_eff/B = k D'(k)/D(k) = weighted average of h(k s),

where h(z)=z/(exp(z)-1), and the weights are proportional to (1-exp(-k s)) mu(ds). The function h decreases from one to zero. If every column has s<=T, then

B h(k T) <= beta_eff <= B.

This is a necessary condition for every such screen. It is not a sufficient fit criterion. With finite nonzero mean column, dominated convergence also gives D(k)/k -> integral s mu(ds) at k->0. Thus beta_eff tends to B at long wavelength. A shallow-law exact spectrum with b<B cannot equal a finite-mean B screen over all positive wavelengths. There is no conflict with finite-range finite-precision approximation.

For the illustrative cap T=23.583, solving h(z)=0.25 gives lambda=21.093 micrometers when B=1. At longer wavelengths the capped screen slope must exceed 0.25, while the uniform b=0.25 target slope is below 0.25. Therefore an independent cap plus a reliable long-wavelength extinction slope would break this particular degeneracy. The cap used here is constructed, not measured. Without an independent cap the alternative can move the departure to a longer wavelength. Emission and dust spectral features can also invalidate this extrapolation.

## Validation and limits

The maximum untruncated spectral discrepancy decreases from 3.72e-8 to 6.03e-9, 1.24e-9, and 2.61e-10 in fractional stellar flux for quadrature orders 64, 128, 256, and 512. Separate transform tests at alpha=0.25, 0.5, and 0.75 give absolute errors below 1e-6. Direct integration of the known alpha=0.5 density agrees with its Laplace transform to 3.4e-16. One thousand fixed-seed random finite mixtures satisfy the cap slope inequality without a positive numerical violation. These checks test the implementation; the proofs give the continuum results.

No claim is made that the stable column distribution is dynamically viable, that arbitrarily high opacity indices are realistic grain physics, or that dust power laws hold outside the tested range. Magnetic, thermal, mass, and gas-column constraints could rule out alternatives. The same is true for spatially resolved constraints or a known cloud shape. More colors can reject a particular parametric screen and reveal opacity features outside a pure power law. The result shows why broad color precision alone does not identify an intrinsic index in the free-column model. It does not dispute the gas evidence, measure a grain size, resolve the material supply, or turn host persistence into a dust residence time.

## Reproduction and provenance

Use Python 3.12 with numpy, scipy, matplotlib, and beautifulsoup4. Set numerical library threads to one. The run used Python 3.12.16, numpy 2.5.4, scipy 1.18.1, and matplotlib 3.11.2. From the verified, extracted publication root:

```sh
python files/retrieve.py /tmp/cpv-external-4ce71
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --source /tmp/cpv-external-4ce71/article.html --out /tmp/cpv-results-4ce71
```

The retrieval code checks the exact source hash. Alternatively use the existing shared file in place: `/mnt/dell-data/shared_datasets/cpv-bouma-2609.00136v1-html/article.html`. Its resolved path is recorded in `files/results.json`. Source URL, version, and SHA-256 are in `files/NOTICE.txt`. No new dataset was downloaded or added. Do not write outputs into the signed publication. Compare `results.json`, `spectra.csv`, and `hierarchy.png` with the included versions; only the input path can differ. The source spectra file contains predictions from our constructed models, not extracted observations. All computations finish in seconds with one process and need no service.
