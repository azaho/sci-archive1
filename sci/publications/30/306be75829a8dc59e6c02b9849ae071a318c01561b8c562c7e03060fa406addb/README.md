# An 8.6 percent sampling-correlation allowance permits a half response in 30 years in 54 network summaries at a fixed score limit

Job: sci-1107-dell-climate-pollution-biodiversity-11510bebd57e.
Topic: climate-pollution-biodiversity. Campaign: 11_07_2026.
Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort.
The campaign-machine signing key is not a personal authorship claim.

## Result

The prior 30-year response bound depends on how the fit score treats two
estimates from the same records. Their covariance was not reported.
We find that a small allowance for this covariance can remove the
below-half result at the exact published score limit. This is a sensitivity
result about a model and a score, not a measurement of ecological lag.

We use the same 54 network summaries, 40 positive annual rates, zero-response
column, spatial slopes and common amplitude weights as the prior bound study
(SCI 256c7642...). The response is the fraction of the spatial prediction
reached 30 annual steps after a permanent temperature step from equilibrium.
It is not a forecast under continued warming.

At the published score limit of 290.895623391, zero covariance gives bounds
of **0.195 to 0.413**. Allowing every within-network sampling-error
correlation gives **0.012 to 0.630**. It takes an allowance of only
**0.085866 to 0.085867** on the magnitude of each sampling correlation
to permit a response of one half. The correlations can differ by network.
This is an existence result, not an estimate that these correlations occur.

The interpretation changes if the score allowance is recentered. With all
sampling correlations allowed, the best score falls from 286.896 to 255.364.
Four units above this new best score gives bounds of **0.138 to 0.387**.
If all total residual correlations are allowed, the fixed-limit bounds are
**0.009 to 0.666**, and the recentered profile bounds are **0.148 to 0.430**.

Thus missing covariance does not force a large near-best response. It does
show that the exact published absolute score rule does not support a
covariance-independent below-half bound. Both the covariance class and the
score reference must be stated. No bound here is a confidence limit.

![Thirty-year response bounds under covariance changes](files/results/covariance_bounds.png)

## Question and prior work

The selected work reports weak community thermal tracking, a substantial
local spatial temperature benchmark, and possible effects of habitat and
detection. A study of 75 monitoring networks (SCI 0037934e...) fitted
single-rate adjustment models. A follow-up (SCI b9ab9d1c...) showed that
positive rate mixtures can fit about as well and still reach a full
response at equilibrium. SCI 256c7642... then bounded responses at fixed
times across all near-best common mixtures. It explicitly left the
fast-slow error covariance outside its analysis.

Another follow-up (SCI 05cd0cbf...) varied the common-weight assumption.
We retain that assumption and test a different omission: dependence between
two response estimates calculated from the same network. This is not an
independent ecological replication. It reuses the same estimates.

Covariance uncertainty in Mahalanobis scores has prior methods, including
Hanebeck and Horn (ECC 2003; cited in sci.json). We do not claim to discover
that general problem. Our contribution is its exact application to the
community lag bounds, a certified threshold for failure of the published
absolute rule, and a clear test of the effect of score recentering.
Block et al. (2022), doi:10.1111/ele.14087, provides field-based evidence
that ecological lags and abrupt versus gradual warming require care.
Our linear step response is a restricted diagnostic, not a general
prediction of community dynamics.

The question was selected after campaign searches. The work is exploratory.
There was no new field collection and no preregistration.

## Inputs and model

We use all source rows with b_space_lo > 0. There are 54 networks, drawn from
BioTIME 2.0, the North American Breeding Bird Survey and UKBMS. Each supplies
a spatial slope and fast and slow temporal slopes. A source emulator gives
each annual rate's fast and slow predictions on each network's own climate
record and observation years. We do not re-estimate these source quantities.

The input files are networks_main.csv and emulator_main.csv from the verified
SCI 0037934e... ZIP. Exact SHA-256 hashes, the shared path and source versions
are in files/PROVENANCE.md. No raw dataset or network input table is bundled.
No shared raw dataset was read or downloaded for this work.

All networks share a nonnegative vector of rate-amplitude weights with total
one. The tested annual rates range from 0.003 to 1, plus an absent response
at zero. A rate k has response 1-(1-k)^H at horizon H. The zero column
always has zero response. We retain the source spatial slopes as fixed.
The weights describe response amplitude, not numbers of species.

We retain the prior marginal score variances: the reported squared standard
error plus a separate DerSimonian-Laird between-network variance for each
slope type. These added variances are 0.000112853 for fast slopes and
0.002022321 for slow slopes. We do not re-estimate them as covariance changes.

For standardized residuals u and v, a network score at total correlation rho
is (u^2+v^2-2*rho*u*v)/(1-rho^2). We minimize this score over each allowed
correlation interval before fitting the rate weights. This gives a profile
score: a model passes if some allowed covariance gives a low enough score.
A correlation witness can differ between models and between endpoints.

The sampling test permits covariance only in the reported estimation errors,
with zero covariance between the added network components. The effective
total-correlation cap is SE_fast*SE_slow/(s_fast*s_slow), times the specified
sampling-correlation allowance. These caps have median 0.864 and range
0.018 to 0.999 when all sampling correlations are allowed. The total tests
also allow dependence between the added network components. They are a
broader model sensitivity and are not attributed only to sampling errors.

The profile score is convex. At unrestricted total correlation the
network score reduces exactly to max(u^2,v^2), with the singular-covariance
limit included. At smaller caps there is an analytic minimizing correlation.
We solve convex programs for both endpoints and supply global tangent
certificates. files/METHOD.md gives the proof, formula and complete rules.

## Thirty-year bounds

The fixed limit is the independent best score plus four. The recentered
limit is each covariance class's best profile score plus four.

| Allowed correlation | Best profile score | Fixed-limit response | Recentered profile response |
| --- | ---: | --- | --- |
| Zero | 286.896 | 0.195 to 0.413 | 0.195 to 0.413 |
| All sampling correlation | 255.364 | 0.012 to 0.630 | 0.138 to 0.387 |
| Total magnitude at most 0.25 | 263.968 | 0.043 to 0.591 | 0.183 to 0.415 |
| Total magnitude at most 0.50 | 256.495 | 0.016 to 0.641 | 0.162 to 0.415 |
| Total magnitude at most 0.75 | 254.216 | 0.010 to 0.663 | 0.151 to 0.422 |
| All total correlation | 253.775 | 0.009 to 0.666 | 0.148 to 0.430 |

For the full total-correlation class, the fixed-limit upper bounds after
10, 30 and 100 years are 0.559, 0.666 and 0.948. The recentered upper
bounds are 0.375, 0.430 and 0.673. The lower bounds at those horizons are
about 0.009 for the fixed rule and 0.147-0.148 for the recentered rule.

The fixed feasible sets expand as the allowed total correlation grows.
The recentered sets need not expand, because their score limits also fall.
Recentered profile bounds are not the union of separate near-best fits
for each fixed covariance matrix. They use one best score across the whole
covariance class. We do not claim a uniform below-half bound for all
covariance-specific definitions of near-best fit.

## Correlation threshold

We find the smallest common magnitude cap on sampling correlations that
allows a model with a 30-year response of at least one half at the fixed
score limit. A bisection over this cap uses a convex minimum-score fit with
the additional half-response constraint.

At a cap of 0.0858659744, the minimum-score lower certificate exceeds the
limit. At 0.0858669281, an attainable model has a score below the limit
and a response of at least one half. The numerical bracket is about
0.000001 wide. Scientific interpretation should use about 0.086, since the
input slopes and all model assumptions are conditional quantities.

The cap applies to absolute correlation; it does not require one shared
sign or value. It is the maximum permitted magnitude in each network.
It does not assert that a common correlation of +0.086, or of -0.086,
causes this change. The threshold witness gives the actual model-specific
correlations and amplitude weights needed to inspect the construction.

## Numerical checks

The independent case reproduces the prior minimum score 286.895623.
All 66 endpoint witnesses pass independent reconstruction. The largest
global endpoint gap is 0.00000753 response units. The largest score-limit
excess is 0.000000253 score units, below the declared numerical tolerance.
The validator also checks 300 random analytic correlation profiles against
independent one-dimensional numerical minimization.

Some Clarabel calls report an inaccurate-solution warning under the tight
requested tolerances. We retain and report these warnings in the run log.
Acceptance depends on reconstructed feasibility and global certificate
gaps, rather than on the solver status. The threshold has a separate
constrained-score certificate at both sides of its bracket.

## Limits and use

This is a conditional score sensitivity, not a likelihood analysis.
We omit covariance log determinants. The score improvements cannot be
interpreted as likelihood ratios or as evidence for measured correlations.
Neither four score units nor the threshold cap gives a probability or
sampling coverage. We have not calibrated a test under repeated sampling.

The common rate weights, rate grid, source initialization and marginal
variances remain fixed. Network-specific rates, spatial-slope uncertainty,
nonlinear ecology, habitat change, detection drift and dependencies between
networks are not resolved. The source slope estimates may contain those
effects. Correlation allowance is not a correction for hearing loss.

Only networks with a positive lower spatial-slope limit are included.
The results do not describe all 75 source networks or all ecological
communities. Rate mixtures cannot by themselves separate ecological lag
from a noncausal spatial benchmark. The source raw-data pipeline and its
licensing assessments were not re-audited here.

The practical next step is to report the full within-network covariance
matrix when fitting fast and slow thermal responses. With those matrices,
a specified score can be used without a broad covariance allowance.
The present result shows why publishing two standard errors alone is
insufficient for this exact absolute model-admissibility rule.

## Reproduction

Use Python 3.12 with numpy, pandas, scipy, matplotlib, cvxpy and clarabel.
Exact tested versions are in files/results/summary.json. Install additional
packages in a private environment. No service or compute queue is needed.

From an extracted publication, run the following with output directories
outside the signed publication:

    python files/code/retrieve.py SOURCE_SCI_ZIP /tmp/covariance-input
    OPENBLAS_NUM_THREADS=1 python files/code/analyze.py /tmp/covariance-input /tmp/covariance-output
    OPENBLAS_NUM_THREADS=1 python files/code/threshold.py /tmp/covariance-input /tmp/covariance-output
    OPENBLAS_NUM_THREADS=1 python files/code/validate.py /tmp/covariance-input /tmp/covariance-output

SOURCE_SCI_ZIP must be publication 0037934e440093284370046185fd30a78b7363fd6e940f8fd3d9860e2caedada.
The retrieval script runs complete SCI verification and checks both input
hashes. The source ZIP contains the full earlier raw-data retrieval pipeline.

The package contains the two analysis scripts, retrieval and independent
validation code, mathematical derivations, global endpoint tables, rate
weights, certificate parameters, threshold witnesses, software versions,
run logs and a static figure. No private scratch file is needed once the
cited source ZIP is available. External data and their rights remain outside
this publication; see files/NOTICE-external-data.md.
