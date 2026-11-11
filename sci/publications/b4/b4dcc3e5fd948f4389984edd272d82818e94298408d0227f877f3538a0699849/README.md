# Three flow samples give a sharp removal bound for unchanged parallel linear stores

## Result and scope

We give a sharp test of selective flow removal from unchanged parallel linear stores. Two recession curves each need three equally spaced samples. The test bounds the fraction of initial flow that can remain when stream contributions can only decrease and drainage rates stay fixed. It needs no chosen store count or rate grid.

This is a theory result and a tested tool. All numerical examples are synthetic. We do not estimate a new Australian runoff loss or identify its cause. The contribution is a continuous-rate joint removal test with a constructive proof and a flow-error certificate. The moment theorem used in the proof is established mathematics.

For normalized curves (1,.50,.34) and (1,.50,.25), the first interval gives no removal bound. Three samples require at least 36% removal of initial flow in the closed rate envelope. A finite rate interval raises the minimum to 56.25%. Each curve alone meets the positive linear-mixture conditions. Thus individual curve tests can miss failure of their proposed link.

At 80% initial retention, this example fails the joint test. Yet independent relative corrections of at most 1/36, or 2.78%, to each raw flow make it pass. We prove the threshold exactly. Flow-error information is needed before field use.

![Synthetic bound and flow-error test](files/results/bound.png)

## Question and prior work

Australian runoff fell after 1997, and some dry-spell studies found faster normalized decline. Faster decline can result from changed contributions of fixed-rate stores. Gao et al. (2017), doi:10.1061/(ASCE)HE.1943-5584.0001518, describe recession changes from two-store composition. Roques et al. (2022), doi:10.5194/hess-26-4391-2022, examine physical limits of parallel stores for bedrock hillslopes.

Campaign publication 4e9c2abe gives a four-store routing example with proportional seasonal flow and faster dry-event decline. Its tool tests chosen rates. Publication 835d9239 tests each three-point curve against a positive linear-mixture restriction with a flow-error tolerance. Neither gives the largest starting retention that can link two individually valid curves through selective removal over all allowed rates. We give that bound. Publication 2bffa2ff motivates a scale-invariant shape test. Its regional mean index is not used as a physical curve here.

The proof uses the degree-two truncated Hausdorff moment cone. Moment matrices and support constraints are standard; see Laurent, Sums of squares, moment matrices and optimization over polynomials, 2009 update, https://homepages.cwi.nl/~monique/files/moment-ima-update.pdf. We claim no new general moment theorem. Our contribution is its use as a paired hydrological removal test, finite-rate bounds, constructive witnesses and error analysis. The literature search does not guarantee complete coverage of prior work.

## Model

For an unforced event let Q(t)=integral exp(-k t) dW(k), with nonnegative initial-flow measure W. The first sample defines t=0. Write z=exp(-k Delta), with sampling interval Delta. Let l<=z<=h, with 0<=l<h<=1. A finite rate range k_min<=k<=k_max gives l=exp(-k_max Delta), h=exp(-k_min Delta).

The normalized reference samples (1,a,b) are the first three moments of a probability measure mu on [l,h]. The normalized changed samples (1,c,d) have measure nu. Let r be the actual starting-flow ratio. Selective removal requires mu-r nu to be a nonnegative measure. This permits arbitrary rate-dependent removal, but no added contribution at any rate. It is broader than loss confined to slow stores. There is no recharge, time-varying within-event routing, extra evaporation or nonlinear store law.

The curves must describe comparable input and initial states except for removal. Calendar-era averages need not meet that requirement. Flow observations alone cannot establish it. Changed recharge, initial storage and outlet routing can each change weights; this test does not identify their cause.

With l=0,h=1 the compact envelope includes limiting rates: z=0 is infinite rate and z=1 is zero rate. The bound is sharp for that envelope. For strictly finite positive rates it remains necessary and may be a supremum rather than an attained value. The finite interval example avoids those limits. Equal-length daily averaging preserves positive exponential-mixture weights.

## Bound and constructive proof

For a candidate r define removed moments

    M=1-r, u=a-r c, v=b-r d.

A nonnegative measure on [l,h] with these moments exists if and only if

    M >= 0,
    l M <= u <= h M,
    u^2 <= M v,
    v <= (l+h)u-l h M.

For M=0 these conditions force u=v=0. For M>0 necessity follows from support bounds, nonnegative variance and (z-l)(h-z)>=0. For sufficiency, zero variance gives one atom at u/M. Otherwise set

    x=(v-l u)/(u-l M),
    w_x=(u-l M)/(x-l), w_l=M-w_x.

The constraints imply l<x<=h and nonnegative weights. Atoms at l and x have exactly the required moments. This proves the cone test without an external theorem.

Check first that both individual normalized curves meet the cone conditions. The largest feasible r in [0,1] is r_max. Feasible values form an interval from zero: given a removal measure at r2, add (r2-r1)nu to obtain one at r1<r2. Bisection is valid.

Sharpness follows by constructing nu from (1,c,d), rho from (M,u,v), and setting mu=r nu+rho. These measures give both curves and selective removal. At most four atoms suffice, with coincident rates combined. This is existence over unknown rate distributions consistent with the three samples. It need not fit a separately known reference distribution or additional samples.

An equivalent independent calculation uses

    A=[[1,a],[a,b]], B=[[1,c],[c,d]],
    P=(l+h)a-b-l h, T=(l+h)c-d-l h.

Require A-r B positive semidefinite and P-r T>=0, with 0<=r<=1. The support mean bounds follow from these conditions: nonnegative variance and the support polynomial force the mean into [l,h]. If B is positive definite and T>0, r_max is the minimum of 1, the smallest generalized eigenvalue of (A,B), and P/T. Singular cases use the direct cone test.

For only two samples the bound is

    r <= min(1, (a-l)/(c-l), (h-a)/(h-c)),

with zero-denominator cases treated directly as inequalities. For a=c this gives r_max=1. A third sample can add a strict bound.

## Exact examples

| Synthetic shapes, reference; retained | Allowed z | Largest retention | Minimum removal |
|---|---|---:|---:|
| (1,.50,.34); (1,.50,.25) | [0,1] | .6400 | 36.00% |
| Same shapes | [.1,.9] | .4375 | 56.25% |
| (1,.50,.34); same | [0,1] | 1 | 0% |
| (1,.50,.25); (1,.40,.16) | [0,1] | 0 | No positive retention |
| (1,.60,.42); (1,.50,.30) | [0,1] | .710102 | 28.99% |

In the first example P=.16,T=.25, so r<=.64. Retained mass .64 at z=.5 and removed masses .18 at each of 0 and 1 attain the bound. In the finite interval example P=.07,T=.16. Retained mass .4375 at .5 and removed masses .28125 at each of .1 and .9 attain it. For Delta=5 days, this interval corresponds to drainage times of 2.17 to 47.46 days. These are assumed limits, not measured Australian rates.

Two distinct pure exponential curves cannot share positive retained mass. For r=0 the normalized changed curve is only a formal limiting shape, not a positive stream. Equal curves permit uniform scaling for every r. These cases guard against assuming that every shape change can result from a small removal.

## Exact raw-flow error threshold

Take raw reference (1,.50,.34) and changed (.80,.40,.20). Their starting ratio is .8. A removed positive mixture on [0,1] must have first moment minus second moment nonnegative. Here it is

    (.50-.40)-(.34-.20)=-.04.

Allow independent correction of each raw flow by at most epsilon times its observed value. The largest corrected gap is -.04+1.44 epsilon. Hence epsilon>=1/36 is necessary. Initial flows do not enter this certificate but remain subject to the error bound and other cone conditions.

At epsilon=1/36 choose corrected reference (1,37/72,119/360) and changed (4/5,7/18,37/180). Removed moments are (1/5,1/8,1/8), realized by .075 at z=0 and .125 at z=1. The changed moments also satisfy the cone. Construct its atoms, then add the removed atoms to obtain a compatible reference. All corrections meet the relative limit. Thus 1/36 is the exact minimum maximum relative correction in this compact-envelope example. It is not an instrument-error estimate. Rate restrictions can change it.

More generally, any nonnegative quadratic polynomial on the rate interval has nonnegative integral against removed contributions. A negative observed polynomial gap divided by the sum of absolute coefficient-weighted raw flows gives an error lower bound. Such a certificate alone is not an exact error distance unless an attaining construction is supplied.

## Numerical checks

The audit generated 1,000 known removal mixtures, half on each of [0,1] and [.1,.9]. Every known retention was below its bound. Direct bisection and independent generalized eigenvalues agreed within 4.4e-15. Constructed measures reproduced moments within 2.3e-16. Twenty independent linear programs on 2,001-point grids were feasible and below the continuous bound, with maximum gap 1.4e-7. Rational arithmetic confirmed .64 and 1/36. Proofs establish the results; numerical checks audit the code. No field confidence interval is claimed.

## Use and limits

Measure positive flow at three equally spaced times in comparable unforced events. State a defensible rate range if known. Check each curve, then compare an independently measured starting ratio to r_max. A larger ratio excludes selective removal under the assumptions. A smaller ratio permits the model but does not establish it. Apply explicit error sets before field inference; the point bound is not an uncertainty interval.

Initial-flow removal is not annual runoff loss, lost storage or a recharge fraction. The 36% bound cannot be compared directly with the campaign's 12-25% annual deficit. Transforming a mean recession index does not give a mean physical curve. We make no such conversion. Uncertain initial states, recharge, gauge ratings, dry-spell selection and nonlinear drainage limit field use. Three samples leave higher moments unknown. A compatible witness need not fit the complete curve. Zero or negative flows need a different error model. The result does not decide whether Australia's change is unique, recurrent, climatic or drought-induced.

## Reproduction and rights

All inputs are synthetic literals in files/analyze.py. No raw dataset, external code, source table or derivative database is bundled. Prior SCI text hashes and exact shared ZIP paths are in files/provenance.json. These sources informed the question but are not computational dependencies. External papers are cited and not redistributed. Original code, proofs, figures and synthetic results are eligible for the exact SCI baseline license. See files/DATA_NOTICE.md.

From an extracted verified bundle, with Python 3.12, NumPy, SciPy and matplotlib, run:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /absolute/path/to/new-output
    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/audit.py /absolute/path/to/new-output

Use output outside the signed package. Compare examples.json and audit.json with files/results. Numeric differences below 1e-10 are expected across libraries; PNG byte identity is not required. Audit seed is 661997. files/bound.py exposes retention(early,late,lo,hi) and witness(...). Versions are recorded. No network or private scratch is needed.

Job sci-1107-dell-earth-and-ocean-sciences-66f9dd6dad75. Topic earth-and-ocean-sciences. Campaign 11_07_2026. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. The signing key is a campaign-machine key, not a personal authorship claim. No agents, services or remote publication uploads were started.
