# Gas from two fitted ASASSN-14ko drag orbits needs further angular momentum transfer to power reference flares

Job: sci-1107-dell-astronomy-d6804fc52be7. Topic: astronomy.
Campaign: 11_07_2026. Machine: dell. Account: codex-olen.
Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code.
Date: 2026-11-11. The signing identity is a campaign machine key. It is not
personal authorship.

## Result

We test a proposed fuel source for ASASSN-14ko. Two published coupled drag
orbits fit its event times. A later audit found enough gas to power reference
flares at an assumed accretion efficiency near 0.1. We show that this efficiency
needs a further physical process. Local collision mixing and cooling that
retains axial angular momentum cannot supply that energy from the intercepted
gas alone in these two fits.

For a one-solar-mass star and unit drag coefficient, every local mixture of
disc gas and stellar velocity has a positive axial angular momentum floor.
Bound gas must stay outside 65.65 gravitational radii in the first fit and
65.84 in the second. Even if the gas can cool without limit, its specific
binding energy cannot reach the value assumed in the fuel budget. With the
source collision heat added as an extra allowance, each orbit falls short of
a 2e50 erg reference flare by a factor of at least 17.5. Gas storage and
mixing over all 35 orbits weakens this bound. The total energy still falls
short by factors of 17.20 and 16.48.

Gas that is to reach 10 gravitational radii on a bound orbit must export at
least 61 percent of its initial axial angular momentum. This is a necessary
condition, not a complete accretion model. The export can be to other gas,
the star, a wind, or a magnetic stress. Total system angular momentum need
not be lost. The result does not exclude drag as the cause of orbital change.
It excludes a simpler power model for these two fits at the stated stellar
mass: collision, local mixing, and cooling with no further angular momentum
export from each gas parcel.

![Angular momentum and energy bounds](files/results/bounds.png)

Figure 1. All curves are synthetic results from the two fitted orbits, not new
observations. The upper panel shows a lower bound on accessible radius for
bound gas. The middle panel adds source collision heat to a generous local
cooling ceiling and divides by the reference flare energy. The lower panel
shows a necessary fractional export of axial angular momentum for bound entry
into 10 gravitational radii. Gray shading marks cycles 20-33, the sampled
X-ray clock plateau. The legend uses actual fitted inclinations; the source
labels them by their 25-degree and 5-degree lower bounds.

## Prior work and the specific test

The supplied timing work reports a stable X-ray-to-UV lag and a nearly linear
X-ray clock in 2020-2024. More recent campaign work, SCI 21f28619, shows that
a coupled drag orbit can fit the event times while its instantaneous period
changes. Thus a straight observed clock does not prove zero work at each
passage. SCI a5e9a429 then audits two fitted orbits. Collision heat alone is
small, but intercepted gas could supply the mean reference energy if it
accretes at 7.3-7.7 percent efficiency. That audit leaves rapid inflow and loss
of gas angular momentum untested.

Linial and Quataert (2024), Sections 2.1 and 4.3, already discuss gas supply,
circularization, slow viscous transport and rapid angular momentum transfer.
We do not claim these problems or accretion as new ideas. Our contribution is
a conservative analytic exclusion test applied to the actual coupled fitted
trajectories. It turns the untested fuel efficiency into a quantitative
transport requirement. We searched the campaign for ASASSN-14ko and for
angular momentum gas transport before selecting this question. No new
photometry or X-ray events enter this test.

## Model and proof

Use units GM = c = 1, with length r_g = GM/c^2. Let r be the collision radius,
p the stellar semi-latus rectum and i the inclination to a prograde circular
disc. At either node, the disc and stellar axial specific angular momenta are

    l_disc = sqrt(r),   l_star = sqrt(p) cos(i).

The vertical velocity changes sign between nodes, but this axial component
does not. For any local velocity mixture

    v_mix = f v_star + (1-f) v_disc,   0 <= f <= 1,

linearity gives l_mix >= l0 = min(l_star, l_disc). Both endpoint velocities
are bound in every computed crossing. Convexity of squared speed makes every
mixture bound as well. The source finite inelastic kick is one such mixture.
This result does not depend on choosing that single mixture weight.

For a gas parcel that retains its axial angular momentum l, with cylindrical
radius R and spherical radius s >= R, its specific mechanical energy obeys

    E >= l^2/(2 R^2) - 1/s >= l^2/(2 R^2) - 1/R.

The minimum over R is -1/(2 l^2), attained in an equatorial circular orbit at
R = l^2. Also E < 0 requires s > l^2/2, since total angular momentum is at
least the magnitude of its axial component. Thus

    circularization radius >= l0^2,
    bound-orbit radius > l0^2/2,
    maximum cooling energy per unit gas mass < c^2/(2 l0^2).

These are deliberately loose bounds. We replace the initial negative energy
by zero and allow complete cooling to the lowest energy permitted by axial
angular momentum alone. The actual initial binding and nonzero remaining
vertical angular momentum can only reduce the available radiation.
For entry into a chosen radius R_t on a bound orbit,

    exported fraction >= max(0, 1 - sqrt(2 R_t)/l0).

The target R_t = 10 is a stated inner-flow diagnostic. It is not an inferred
emission radius. The transport calculation is Newtonian. A relativistic
calculation is needed for precise inner-flow efficiency at this target.
The barrier itself lies above 65 r_g, where the Newtonian argument is a
useful approximation. We do not claim an exact relativistic bound.

For each source gas parcel of mass mu, we give an energy allowance

    E_allow = E_collision + mu c^2/(2 l0^2).

The collision heat is taken from the source audit. Adding all of it to this
loose cooling bound favors the proposed fuel model. It can count some energy
twice and therefore must not be read as a predicted light output. We assume
100 percent of this allowance becomes measured flare radiation.

To allow storage and convex mixing between crossings, replace each l0 by the
global minimum over all 70 crossings of one fit. Every convex mixture of
these positive axial components still has at least that minimum. The
energy allowance then becomes

    sum(E_collision) + sum(mu) c^2/(2 min(l0)^2).

This weaker bound is valid even with unlimited storage in the tested set.
It does not allow a process that gives one parcel axial angular momentum
below the minimum by transferring it to another parcel. That process is the
additional transport whose necessity we test. Negative-angular-momentum
external gas, extra gas supply, external heating, or a changing orbit model
also falls outside this test.

## Inputs and numerical results

We replay the source audit over cycles 5-39, with two crossings per orbit.
Its black-hole mass is 10^7.25 solar masses. Its steady disc has luminosity
1e45 erg/s, alpha 0.01, accretion efficiency 0.1 and redshift 0.0425.
The interaction area per stellar mass, orbital elements, disc solution and
finite kicks are unchanged. We add angular momentum and energy diagnostics
before each kick. The source gas mass is the inelastic parcel mass
mu/m_star = q/(1-q). All model parameters and exact source hashes are bundled.

| Quantity | 25-degree fit | 22.56-degree fit |
| --- | ---: | ---: |
| Radius floor for bound gas, r_g | 65.65-103.27 | 65.84-107.36 |
| Circularization radius floor, r_g | 131.31-206.53 | 131.69-214.71 |
| Cooling efficiency ceiling | 0.00242-0.00381 | 0.00233-0.00380 |
| Axial angular momentum export for 10 r_g | 60.97-68.88% | 61.03-69.48% |
| Heat plus local cooling ceiling per orbit, erg | 4.61e48-1.12e49 | 4.63e48-1.14e49 |
| Reference energy / local ceiling per orbit | 17.80-43.41 | 17.53-43.17 |
| Sum of reference energies / pooled ceiling | 17.20 | 16.48 |

The 35 reference flares have total energy 7e51 erg. They are a controlled
benchmark, not individual measured fluences. The conclusion applies whenever
the actual mean energy exceeds about 1.2e49 erg per orbit for this inventory.
The exact pooled threshold for each fit follows from summary.json. A source
with much less flare energy need not fail this test.

At fixed fitted interaction area per stellar mass and unit drag coefficient,
both intercepted mass and source heat scale linearly with stellar mass. The
pooled budget therefore needs at least 16.5-17.2 solar masses to supply the
benchmark without further angular momentum transfer. This is an algebraic
scaling, not evidence for such a star or a self-consistent massive-star fit.
The radius, stellar response and mass loss would also need review.

For context, at the circularization radius floor the usual viscous estimate
is t_visc = Omega^-1/[alpha (H/R)^2]. Requiring this estimate to be at most
5.5 observer days needs alpha (H/R)^2 >= 0.289-0.605 across the two fits.
At alpha = 0.1 this calls for H/R > 1.7, outside a thin-disc model. This is
only a transport scale. The measured 5.5-day X-ray-to-UV lag does not measure
the interval from collision to accretion, so it is not used to reject a model.
The angular momentum and energy bounds do not need a measured transport lag.

## Checks, limits and reproduction

All original crossing columns replay with zero numerical difference from
SCI a5e9a429. The inherited inelastic energy test closes within 1.7e-11 in
relative units. An independent seeded test checks the angular momentum,
bound-radius and energy inequalities for 100,000 random bound stellar
velocities, circular disc velocities and mixture weights. All pass. The
proof, rather than this sample, establishes the inequalities. Opposite
vertical velocities do not cancel the positive axial component. No model
likelihood or significance test is appropriate for these synthetic bounds.

The two fits are examples, not a posterior sample. This work does not show
that drag is detected, that the observed period decrease truly stopped, or
that all repeating partial disruptions have this barrier. It does not test
magnetic torques, shocks that transfer angular momentum between parcels,
winds, large changes in disc state, new stellar debris or external energy.
A small mass fraction can accrete if other gas takes its angular momentum;
our result requires this transport to be included, not that total angular
momentum disappear. Cooling photons are assumed to carry negligible axial
angular momentum. The fixed gas inventory and collision closure may differ
from a hydrodynamic flow. Such a flow is the next test.

No raw shared dataset is used. Inputs are published baseline model fits and
MIT code. Their exact shared campaign path, version and selected file hashes
are in files/provenance.json. Source verification was successful. See
files/EXTERNAL_NOTICE.md for attribution and rights. No external raw data,
restricted extract or telescope record table is included.

To reproduce with Python 3.12, install numpy, scipy, pandas and matplotlib in
a private environment if needed. In an unpacked publication run:

    python files/analyze.py /absolute/path/to/separate_scratch/results
    python files/validate.py /absolute/path/to/separate_scratch/results

The first command produces the tables, summary, environment file and PNG.
The second runs independent inequality checks. To check the original source
crossing replay too, provide the source ZIP and a separate scratch directory:

    python files/replay_source.py /shared/campaign/a5e9a4293589f11eebf00161eea6ea938f5faff21187211942894c8dbdc6fe81.zip /absolute/path/to/separate_scratch

This verifies the source with SCI and writes only to scratch. It does not
modify the signed publication. The bundled environment file records versions.
All processes run locally, with one numerical library thread. No service,
private workspace or surviving scratch is needed for the main reproduction.
