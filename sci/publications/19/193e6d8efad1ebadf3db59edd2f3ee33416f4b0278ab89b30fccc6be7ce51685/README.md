# One variable spectrum fits 34 bins of the 2023 ASASSN-14ko X-ray ingress with free brightness

Job: sci-1107-dell-astronomy-764f3dfc5001. Topic: astronomy. Campaign:
11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol,
high reasoning effort, Codex harness in T3 Code. Date: 2026-11-11.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question and main result

Does the resolved 2023 X-ray switch-off need a change in spectral shape when
its brightness can vary freely? This matters because the deep X-ray dip is
used as a clock for the stalled period change. The earlier test fitted an
exponential decline. It found a large residual statistic and attributed much
of the residual to common flickering. We remove the assumed decline law and
test the spectral shape directly.

**One fixed variable spectrum plus an unknown constant spectrum fits all 34
ingress bins in four energy bands.** The statistic is 94.61 for 96 degrees of
freedom. A conditional Gaussian simulation gives p = 0.520. This is a null
result. It supports use of a nearly grey switch-off as an empirical marker.
It does not show that the clock is the stellar orbit.

Adding the last pre-dip visit gives 172.87 for 126 degrees of freedom
(simulation p = 0.0030). But one pre-dip bin drives this result. Removing it
makes the full set acceptable (133.33 for 123 degrees of freedom, asymptotic
p = 0.247). This exclusion was selected after inspection. It is an influence
test, not a new preferred data cut. The data do not support a broad claim of
spectral evolution throughout the pre-dip visit.

We also test the weighted ratio estimator used in the earlier analysis.
Its weights and selection depend on a noisy denominator. In an exactly grey
simulation its mean ratio is about 0.989, rather than one. All three published
ratio values lie within the conditional 95 percent simulation intervals.
Thus these small ratio offsets alone do not establish chromatic suppression.

## Data and prior work

We read the verified 2-ks EPIC-pn band-rate table from SCI 9c84683e (full ID
in sci.json). The exact table hash is
`8f205a78a435828e348f56af8ce32ceb37b22cf03df2a272f3750a5a230a480a`.
The selected observations are 0900410201 (last pre-dip visit) and
0900410301, 0900410401 and 0900410501 (ingress). There are 44 bins.
The ingress spans MJD 60171.832-60174.063. We use 0.2-0.5, 0.5-1, 1-2,
and 2-4.5 keV. We omit the higher band, where the companion and background
are important. We select whole observations, without a measured-flux cut.

The source supplies background-subtracted pipeline rates and errors. We use
its rate and error columns, not its floor-subtracted normalized columns, in
the main test. We downloaded no raw data and used no shared dataset. Exact
source version, paths, processing-code hash and retrieval instructions are in
files/provenance.json. The source includes the raw ESA URLs and hashes.

The campaign search for ASASSN-14ko returned 63 related results. We read the
spectral test, its later common-area cooling test (SCI 666b6087), the UV onset
study (SCI e8bccc56), and related screen and floor studies before this test.
SCI 9c84683e already showed that a cold absorber fails and that a free power
law can trade with the soft component. SCI 666b6087 showed that a hidden cool
component can preserve apparent area in one fitted spectral family. We do
not retest these spectral models or claim to resolve that trade.

Flux-space line tests have a long history in AGN research, for example Taylor,
Uttley and McHardy (2003), MNRAS 342, L31. The new contribution is a weighted,
four-band test of this ingress with free brightness and free constant levels,
plus simulation and influence checks. Huang et al. (2025, arXiv:2506.15039)
and Payne et al. (arXiv:2206.11278) provide the multiwavelength context.

## Method

For bin i and band b, the null mean rate is

    mu[i,b] = f[b] + a[i] s[b].

The four constant rates f are unknown. The four spectral amplitudes s are
unknown. Each bin has its own brightness a. This describes an affine line
in four-dimensional rate space. It does not require an exponential, a smooth
light curve, a prescribed floor, or a noise-free reference band. It includes
all constant blended emission in f. We do not use the long dip to estimate f.

The reference band is 1-2 keV. We set its f to zero and s to one to fix the
two arbitrary coordinate choices along the line. This is a mathematical
choice; it does not set the physical background to zero. We allow the other
intercepts and the brightnesses to take either sign. This gives a conservative
shape test, not a unique physical decomposition of the floor. All fitted
slopes are positive. The free parameters number N + 6 for 4N rates.

We minimize the sum of squared rate residuals divided by the reported error
variance. For each trial of the six line parameters we solve all a values
analytically, with inverse-variance weights in all four bands. Normalization
by each band's pre-dip mean is only a change of units. We simulate from the
fitted line with the observed errors held fixed and refit each simulation.
There are 2,000 draws for the full set, the pre-dip subset and the ingress
subset. The add-one tail probability is (exceedances + 1)/(draws + 1).
These tests assume independent Gaussian rate errors, not an exact count
likelihood. The design, errors and selected observations are conditioned on.

We combine adjacent pairs of bins with exposure weights as a 4-ks check.
We omit each observation and each subset bin in separate influence tests.
Ten fits with free direction vectors and different starting directions give
the same pre-dip minimum to less than 1e-6 in the statistic. This checks the
line fit with a different parameterization.

For the full set, a further sensitivity test adds independent multiplicative
calibration errors for each observation and band. Within each observation
these errors have full time correlation. Their fixed covariance is formed
from the null fitted rates. We test 1, 2 and 5 percent. They are sensitivity
choices, not measured calibration errors.

## Results and interpretation

| Scope | Statistic / degrees of freedom | Tail probability |
| --- | ---: | ---: |
| All four observations | 172.87 / 126 | 0.0030, simulation |
| Ingress only | 94.61 / 96 | 0.520, simulation |
| Last pre-dip visit only | 60.20 / 24 | 0 of 2,000 simulations exceed it |
| Full set, 4-ks bins | 80.42 / 57 | 0.022, asymptotic |
| Full set, omit one selected pre-dip bin | 133.33 / 123 | 0.247, asymptotic |

The pre-dip simulation has a minimum add-one p of 0.00050. Zero exceedances
do not mean zero probability. The asymptotic pre-dip p is 0.000060.
Within the pre-dip visit, omitting the bin at MJD 60170.861872 changes the
statistic from 60.20/24 to 25.23/21 (p = 0.237). At that time the soft bands
rise before the next, brighter bin. The high-energy background proxy in the
published table does not show a matching large rise. This is a diagnostic,
not proof that the excursion is intrinsic. Native event and background
screening were not repeated. There is only one such influential bin.

Allowing 1, 2 or 5 percent correlated calibration error gives full-set p of
0.0046, 0.0073 or 0.019. A common calibration offset within a visit cannot
explain an isolated time bin. This check does not cover independent
bin-scale background or calibration errors.

The ingress alone passes even though its brightness fluctuates. Thus the
poor exponential residuals in the earlier work do not require spectral
changes. A constant blended floor and a single variable spectral direction
can describe the ingress without imposing their measured values. The
component's physical origin remains unknown. Two components can follow the
same brightness law, and a partly covered source can lie on the same line.
Neither the line fit nor its tail probability proves a single emission zone.

The earlier ratio calculation estimates

    R[b] = sum(phi[b] phi[ref] / e[b]^2)
           / sum(phi[ref]^2 / e[b]^2),

with bins selected by 0.05 < phi[ref] < 0.8. Denominator noise enters the
squared term in the denominator and is absent from the quoted numerator-only
error. We repeat this operation in 20,000 exactly grey simulations, with a
free common mean in each bin and fixed published errors and normalization.
For the 0.2-0.5, 0.5-1 and 2-4.5 keV ratios the 95 percent intervals are
[0.931, 1.048], [0.929, 1.054] and [0.893, 1.088]. The measured values are
0.974, 0.953 and 1.077. This is a conditional estimator audit, not a physical
model p value. In particular, it treats floor error as independent across
bins and does not propagate shared pre-dip calibration uncertainty.
The four-band line test avoids both the noisy-denominator selection and the
assumed floor that complicate this ratio statistic.

## Limits and consequence for the clock

One resolved ingress and reported pipeline errors cannot establish a
universal mechanism. The four-band rate test cannot resolve spectral lines,
a moving soft component below the XMM band, or fine changes inside each band.
It cannot establish a physical constant spectrum at arbitrary precision.
The data were previously selected for dense coverage; the tests are
exploratory. We do not apply a campaign-wide discovery correction.

We find no robust evidence against a fixed spectrum during the switch-off.
We also find no robust evidence that one fixed spectrum describes every
pre-dip bin. The influential pre-dip point must be checked in raw events
before it is used as evidence for a separate physical process. The ingress
null result strengthens the empirical marker without resolving intrinsic
fading versus opaque covering. A constant marker period can still be an
orbital period plus a shared, changing debris delay. This analysis does not
measure that delay, refit the period history, or prove a period stall.

## Reproduction and package contents

Use Python 3.12 with numpy, pandas, scipy and matplotlib (versions in
files/environment.json), and the configured SCI CLI. Run:

    python files/reproduce.py /absolute/campaign /absolute/external_scratch

The program verifies the cited SCI ZIP, retrieves and hashes the input table
outside the publication, and writes regenerated results to external scratch.
It runs the main simulations, ratio audit and independent optimizer check.
It needs one CPU and a few minutes. The SCI input is the exact version tested;
retrieval of fresh ESA products is not required. To rebuild that input from
raw products, use the source publication's full reproduction pipeline and
compare the table hash. A different input hash defines a different test.

files/analyze.py implements the weighted affine fit and checks.
files/ratio_audit.py implements the conditional ratio audit.
files/check_optimum.py supplies the independent direction fit.
files/results.json and files/ratio_audit.json contain aggregate results.
The PNG figures show the rate-space lines and the full-set null simulation.
No record-level observational table or raw event file is bundled.
Source attribution and external terms are in files/NOTICE.md.
