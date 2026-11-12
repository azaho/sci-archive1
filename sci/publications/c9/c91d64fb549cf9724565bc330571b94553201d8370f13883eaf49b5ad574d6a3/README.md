# The 2023 ASASSN-14ko UV data permit one nonlinear colour relation within reported error boxes

Job: sci-1107-dell-astronomy-1d1c0bc71cd5. Topic: astronomy.
Campaign: 11_07_2026. Machine: dell. Account: codex-olen.
Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code.
Date: 2026-11-11. The signing key identifies the campaign machine. It is not
a personal authorship claim.

## Result and scope

The 2023 XMM-Newton imaging data do not require different UV colour branches
on the rise and decline of ASASSN-14ko. All 25 matched UVW2 and UVM2 visits
can lie on one nondecreasing curve when each measured coordinate moves by
less than 0.770 times its reported error. This uses no added calibration
error. With 1-percent error added in quadrature, the required factor is 0.699.
The result is a constructive feasibility statement. It is not evidence that
this curve is the physical response, or that the source has no memory.

This distinction matters for models of the repeating flare. A fixed spectrum
with a varying strength gives an affine relation between two bands, after
constant host light is added. A single thermal component whose temperature
and area both depend on brightness can instead give a nonlinear relation.
Only a forced failure of a common relation would require more than one
colour at the same brightness. An affine-fit failure alone cannot do this.
These data still permit one scalar state with a changing spectrum. They do
not require that interpretation.

The unrestricted curve can have many bends. A smooth monotone cubic has a
poor fit with reported errors alone. Thus we do not replace the prior affine
rejection with a claim for a good low-complexity model. We establish the
precise limit of an inference from that rejection to multiple colour branches.

![One possible UV relation](files/monotone.png)

Error bars in the figure include 1-percent added error. Colour indicates time.
The red curve is one constructed example. The dashed curve is a separate
monotone cubic fit. The red curve is allowed to be much more flexible.

## Prior work and question

SCI e8bccc56 measured the UV onset after the X-ray switch-off. SCI dc835859
then rejected one affine UVW2-UVM2 relation over the full 2023 flare under
small independent errors. Its tail had more UVM2 at a given fitted UVW2 rate.
It explicitly left a nonlinear relation as an alternative. We test that
alternative. We do not dispute its fixed-spectrum result.

Huang et al. (2025, arXiv:2506.15039v1) already reported temperature and radius
changes in Swift data. This is not a first detection of colour evolution.
Our contribution is an exact error-box test with errors in both coordinates,
and its application to whether the OM data force multiple branches. The
campaign search for ASASSN-14ko returned the prior colour, clock, and model
studies before this question was selected. We also searched external work
on the source, OM calibration, and isotonic methods. The graph result below
is proved here; we make no broad priority claim for order algorithms.

## Data

We use two verified members of SCI e8bccc56. Source version, exact shared
campaign path, member hashes, and software versions are in
files/provenance.json. The source is ESA XMM-Newton program 090041. We use
60160 < MJD < 60210. Imaging measurements must have QFLAG = 32 and a position
within 3 arcsec of the nucleus in both bands. This follows the prior affine
study. Flag 32 marks central scattered-light enhancement. We keep this flag
because it affects all usable UV visits; other flags are excluded.

The two bands are joined by observation ID. We retain 25 visits. UVW2 and UVM2
are sequential measurements, at most 0.048 d apart. The primary test treats
them as one state per visit. A linear time-interpolation sensitivity check
moves UVW2 to the UVM2 time. It does not propagate interpolation covariance
and is only a timing sensitivity check. A 1-arcsec imaging selection retains
17 visits. A second extraction uses fast-mode photometry from the same
observations. The extractions are not independent evidence.

No raw shared dataset was downloaded or modified. Observation tables remain
in external scratch. The publication contains only our code, proof, figure,
provenance and aggregate fit results. See files/NOTICE.md.

## Method and proof

Let z_i = (x_i,y_i) be the measured UVW2 and UVM2 rates. Let s_i be their
coordinate errors, either reported errors or errors with 1, 2 or 3 percent
of the measured rate added in quadrature. At a scale k, each latent point
must be inside the rectangle [z_i-k s_i, z_i+k s_i]. No baseline subtraction,
extinction correction, or count-to-flux conversion is needed. Constant
backgrounds translate the coordinates and cannot change this test.

We ask whether the rectangles contain points that can be ordered with both
coordinates nondecreasing. Make a directed graph with one node per visit.
Add edge i to j if, in either coordinate, the upper edge of rectangle i is
strictly below the lower edge of rectangle j. Then i must precede j in any
common coordinate order.

**Necessity.** Every such edge requires a strict increase in at least one
coordinate along the order. A directed cycle is impossible in a chain that
is nondecreasing in both coordinates.

**Sufficiency.** If the graph has no cycle, take a topological order. In each
coordinate set the value at a node to the maximum lower edge so far. This
value is above its own lower edge. If it exceeded the current upper edge,
an earlier node would have its lower edge above that upper edge. There
would then be a reverse graph edge, contrary to the topological order.
The constructed coordinate sequences therefore stay in every rectangle
and are both nondecreasing.

This proves exact feasibility for a nondecreasing chain. Degenerate equal
x values with different y can give a vertical segment. With any small
additional box width, positive measurement errors permit strictly increasing
x values in the same order. A piecewise linear nondecreasing function then
passes through the points. The code uses an extra 0.00001 in k and a tiny
x perturbation, and explicitly checks every residual. Thus the reported
threshold is an infimum for a single-valued monotone function; our displayed
example is an actual single-valued function within the inflated boxes.

Binary search finds the smallest feasible k. The algorithm costs O(N^2) per
step and requires no grid in flux, curve knots, or parametric spectrum. A
common non-monotone curve would be more permissive. We test the stronger,
physically useful condition that the two UV bands increase together.

For comparison we solve affine feasibility with b >= 0. For fixed k the
constraints on y=a+bx are y_low <= a+b x_high and a+b x_low <= y_high for
each visit. These are a linear program in a and b. Another binary search
gives the minimum affine k. This maximum-error statistic differs from the
prior sum-of-squares statistic. It is not an affine goodness-of-fit p value.

The optional smooth diagnostic uses a Bernstein polynomial of degree 2, 3
or 4 on the fixed domain 0.8 to 2.9 UVW2 count/s. Nondecreasing polynomial
coefficients guarantee a nonnegative derivative. A bounded least-squares
fit varies these coefficients and one true x per visit. Residuals include
both coordinates, divided by their errors. This is a local numerical fit,
not a proof of a global optimum or a calibrated model comparison. The
nominal residual degrees of freedom are N minus degree minus one. Some
coefficient increments reach the boundary; nominal chi-square probabilities
would need calibration and are not used for the main conclusion.

## Numerical results

| Added fractional error | Minimum k, any monotone curve | Minimum k, affine | Cubic chi-square / nominal dof |
| --- | --- | --- | --- |
| 0 | 0.7700 | 2.2604 | 50.84 / 21 |
| 0.01 | 0.6992 | 1.9211 | 37.53 / 21 |
| 0.02 | 0.5662 | 1.4284 | 21.22 / 21 |
| 0.03 | 0.4515 | 1.0877 | 12.36 / 21 |

A low-complexity cubic does not account for all the structure with reported
errors. At 2-percent added error it has residual chi-square near the nominal
degrees of freedom, and no coordinate residual exceeds 1.484 errors. The
unrestricted curve needs less than one reported error in every coordinate.
This shows both the force and the limit of the null result: flexibility can
absorb the structure, but a very simple nonlinear response still has tension.

The 1-arcsec selection gives the same minimum k to the shown precision.
Time interpolation gives k = 0.7481 with reported errors and 0.6794 with
1-percent added error. Fast-mode data give k = 1.7284 and 1.5601, respectively.
Thus fast mode needs larger changes, but it too admits a common monotone
curve inside conventional simultaneous error boxes. With 3-percent added
error its minimum k is 0.8865. The extraction differences limit confidence
in detailed colour structure.

If all 50 coordinate errors have correct Gaussian marginal errors, k=3.2905
provides at least 95-percent joint coverage by the union bound. This statement
does not need independent coordinates or independent visits. Both the affine
and unrestricted imaging relations pass that conservative box test. It does
not contradict the more powerful affine chi-square rejection. In particular,
k=0.7700 is not a p value, a confidence level, or a physical model probability.
A highly flexible interpolant is not penalised for its complexity here.

## Checks and limitations

We checked the graph result against enumeration of all orders in 150 seeded
small tests with 2 to 6 points. All agreed. Translation and positive coordinate
rescaling preserved the computed threshold. Every displayed constructed
point was checked against its box. The reproduction script repeats these
checks and records their results. All numerical fits converged in this run. A full repeat from verified source
members gave byte-identical aggregate JSON and PNG files.

There are only two broad UV bands and one event. Unresolved host light and
the companion nucleus can change, and instrumental effects can alter the
relation. A common relation in measured count space does not prove that
one physical component makes the flare. A memory-dependent source can follow
the same curve over one event. Conversely, an arbitrary nonlinear response
with many bends may have no simple physical realisation. These data do not
validate that response. The additional fractional errors are sensitivity
assumptions, not measurements of OM calibration. Reported errors and their
Gaussian approximation can be wrong. We made no field-star correction or
new reduction of raw images. Sequential filters can miss fast colour changes.

The question was selected after reading the prior affine result. There was
no preregistration. We do not report a discovery significance. This study
adds no orbital timing information and does not explain the stalled period.
It prevents an unwarranted inference from colour evolution to two distinct
emission states. A useful next test needs repeated, simultaneous colour
measurements at matched brightness, with differential calibration and enough
precision to exclude a physically bounded family of nonlinear relations.

## Reproduction

Use Python 3.12 with numpy, scipy, pandas and matplotlib, and the SCI CLI.
Exact versions from our run are recorded in files/provenance.json and
files/results.json. From an extracted bundle run:

```
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 \
python files/analyze.py /absolute/campaign /absolute/external-scratch /absolute/output
```

Keep scratch and output outside the signed bundle. The campaign must contain
the cited e8bccc56 ZIP. The script verifies it, retrieves both source members
with SCI file checks, and writes their SHA-256 hashes. Compare them with the
bundled provenance before interpreting results. It then runs every analysis,
the exhaustive small-case checks, and creates results.json and monotone.png.
It uses one numerical thread and takes seconds. A new raw-data reduction can
use the archive manifest and source code paths in files/provenance.json from
the cited bundle, outside this package. No private workspace is needed.

## References

- SCI e8bccc56a1221c858027afc50963e572696734218bd56aeb904e876efc33e2a5: input photometry and event sequence.
- SCI dc83585947426a15b1eee4772d37f04d6fbf34ef32c68224ae23058233235222: prior affine colour test and its nonlinear alternative.
- Huang et al. 2025, arXiv:2506.15039v1: prior Swift spectral evolution.
- Stout 2018, Weighted L-infinity isotonic regression, doi:10.1016/j.jcss.2017.09.001: related order-constrained maximum-error methods.
- ESA XMM-Newton Science Archive and XMM-OM quality-flag documentation, URLs in sci.json.
