# Two HD 93683 fits give a companion mass floor near 0.25 solar masses without an inner eccentricity cap between epochs

## Result and tested scope

A low-mass third body cannot hide an arbitrary loss of inner angular momentum between two observed epochs. Its own orbit has limited angular momentum. We use this fact to remove a global inner eccentricity cap from a prior companion mass test.

For two published HD 93683 point fits, inner masses of 18 and 15 solar masses, and endpoint eccentricities no greater than the fitted values, a sole third-body torque requires at least **0.2508 and 0.2543 solar masses** in double-averaged quadrupole dynamics. We round the calculated lower bounds down. The inner eccentricity between endpoints is free. The outer period, eccentricity, nodes and photometric inclination branches are free within this model. The outer orbit can respond to the inner torque.

These are conditional necessary bounds, not mass measurements, confidence limits, new companion detections or fits to a triple orbit. The source system already has a reported Be companion. Our result strengthens the logical scope of the mass test: large unobserved eccentricity alone cannot reduce the mass floor to zero in this model when the endpoint eccentricities remain constrained. It does not extend the test to all Newtonian triples.

![Endpoint mass bounds](files/endpoint_bound.png)

The figure shows sensitivity to endpoint eccentricity and normal errors. It imposes no eccentricity cap between endpoints. Lines connect tested scenarios; they do not carry probability weights.

## Evidence and prior work

We searched the campaign for HD 93683 and for eccentricity, angular momentum, torque and mass floors before choosing this question. The source light-curve study (SCI d86cdb9d) fits one inclination drift to Tycho, ASAS-3 and TESS data. The campaign mass study (SCI 3bd1cefd) combines a finite normal change with a maximum normal rotation rate. Its 0.2556 and 0.2594 solar-mass bounds require a global cap on inner eccentricity at the fitted value. That cap is not established by sparse photometry. Its floor tends to zero if that cap tends to one. The exact-force acceleration study (SCI d8e5084d) removes orbit averaging but retains a global angular momentum envelope and a specified companion mass. We address a different gap: a companion mass bound in the averaged model with endpoint constraints only.

The vector secular equations are established results. We checked equations 17 and 21 of Liu, Munoz and Lai (2015), [DOI 10.1093/mnras/stu2396](https://doi.org/10.1093/mnras/stu2396), [version 2 full text](https://arxiv.org/html/1409.6717v2). Their general equations include outer response and octupole terms. We use their quadrupole terms only. Our contribution is the combination of a bounded vector torque, a shortest arc on the outer angular momentum sphere, and an endpoint-based lower bound on inner angular momentum. We do not claim a new precession equation or an exhaustive priority search.

Only the baseline SCI aggregate input is reused. It records two fitted periods, eccentricities and linear inclination models, plus epoch centers. It is not a set of independent inclination measurements. No new photometry, velocities, astrometry or raw shared dataset enters this work. The source ZIP passed complete verification. Its exact shared path, archive hash and input-entry hash are in `files/provenance.json`.

## Assumptions and endpoint geometry

Use an isolated hierarchical triple of positive, fixed point masses, with double-averaged Newtonian quadrupole dynamics. Both semimajor axes and the outer eccentricity are constant. Total orbital angular momentum is conserved. No spin, disk, mass loss, fourth body or other source supplies the plane torque. We do not impose stability or claim that all near-bound systems are well averaged.

Let M=m1+m2, eta=m1*m2/M^2, x=m3/M, and Lc be the circular inner orbital angular momentum. Let j be the dimensionless inner angular momentum vector, e the eccentricity vector, and k the outer unit normal. They obey j.e=0 and |j|^2+|e|^2=1. Set s=L2/Lc, where L2 is the constant outer angular momentum magnitude. Use periods P1 and P2 in the same units.

Photometry permits either sign of the normal. Fold each fitted inclination to I=acos(|cos i|). The minimum directed separation of any true endpoint normals is at least

```
theta = max(0, |I_b-I_a| - delta_a - delta_b).
```

Here delta is a bound on angular error, not a statistical error bar. If endpoint eccentricities are at most E_a and E_b, define j_a=sqrt(1-E_a^2), j_b=sqrt(1-E_b^2). The implementation uses a common endpoint cap E and j_a=j_b=j0. Then a valid dimensionless chord bound is

```
|j(b)-j(a)| >= q = 2 j0 sin(theta/2).
```

This follows from |j(b)-j(a)|^2=(|j(b)|-|j(a)|)^2 + 4|j(a)||j(b)|sin(angle/2)^2. Thus smaller endpoint eccentricities are allowed. There is no assumed bound on eccentricity inside the interval.

## Proof

In the stated model the inner vector equation is

```
dj/dt = C [(j.k) j cross k - 5(e.k) e cross k],
C = (3*pi/2) (P1/P2^2) [x/(1+x)] (1-e2^2)^(-3/2).
```

Set Q=j j^T - 5 e e^T. The vector in brackets is (Qk) cross k. Q has eigenvalues -5e^2, 0 and 1-e^2. For a real symmetric matrix and a unit vector k, |(Qk) cross k| is at most half its spectral range. One proof treats its square as the variance of the eigenvalues with weights equal to the squared components of k; a variable in an interval has variance at most one quarter of the squared interval width. Hence

```
|dj/dt| <= C (1+4e^2)/2 <= (5/2) C.             (1)
```

Unlike the bound for a unit normal, (1) stays finite as e tends to one.

Conservation gives j(t)+s k(t)=constant. Therefore |j(t)-j(a)|<=2s and |j(t)|>=max(0,j0-2s) for every intermediate time. Inserting this lower bound in (1) gives

```
|dj/dt| <= C B(s),
B(s) = [5-4 max(0,j0-2s)^2]/2.                  (2)
```

There is a second consequence of conservation. The path of j lies on a sphere of radius s centered at the conserved total vector. Its endpoints have chord at least q. Necessarily 2s>=q, and the length of any such path is at least the shorter great-circle arc:

```
2s asin(q/(2s)) <= integral |dj/dt| dt <= C B(s) T. (3)
```

Extra turns can only increase the path length. The statement remains valid if the inner angular momentum passes through zero; it does not divide by |j|.

In period units the angular momentum ratio is

```
s = x/[eta (1+x)^(1/3)] (P2/P1)^(1/3) sqrt(1-e2^2).
```

Put y=2s/q>=1, eliminate P2 in (3), and define

```
f(y) = y^7 asin(1/y),
B(y) = [5-4 max(0,j0-q y)^2]/2,
H(q,j0) = inf_(y>=1) f(y)/B(y).
```

A necessary condition is

```
x^7/(1+x)^3 >= eta^6 q^7 P1 H(q,j0)/(96*pi*T)
                  * (1-e2^2)^(-3/2).            (4)
```

Since the eccentricity factor is at least one, omitting it gives an outer-eccentricity-independent mass floor. The circular outer orbit is the weakest case of these necessary inequalities. The left side increases strictly for x>0, since its logarithmic derivative is 7/x-3/(1+x)>0. Its unique positive root times M is the mass floor. Equality of the inequalities need not be attainable by a physical triple.

A simpler analytic result replaces B by 5/2. The minimum of f is 1.523216718 at y=1.004684351. Write z=asin(1/y); its unique stationary minimum solves 7z cot(z)=1 for 0<z<pi/2. This gives floors of 0.2234 and 0.2267 solar masses, already without a global eccentricity cap. Conservation in (2) strengthens them to the main values.

## Numerical bounds and checks

We bound H with an explicit partition of 1<=y<=2 into 200,000 cells. On each cell B increases, so min(f)/B(right endpoint) is a lower bound. The minimum of f on a cell is an endpoint value or the single stationary value above. For y>=2, f/B>=y^6/(5/2)>=25.6, so that tail cannot lower the reported values. A local minimum supplies an upper bracket, not the lower bound. The lower estimates include a 1e-12 relative downward margin. This is analytic bracketing evaluated in double precision, not formal interval arithmetic. The lower and upper inferred mass brackets differ by less than 7.2e-8 solar masses. We report only four decimal places, rounded down.

We test every epoch pair and keep the strongest floor. Both fits select 2002.5920736 to 2026.0423867, a 23.4503131-year interval.

| Fit | Folded change (deg) | Chord q | Mass floor (solar masses) | Circular period at relaxed optimum (yr) |
|---|---:|---:|---:|---:|
| Joint least squares | 7.78507 | 0.130817 | 0.2508 | 0.48448 |
| Free Tycho offset | 7.90081 | 0.132756 | 0.2543 | 0.48572 |

The periods are not fitted periods or allowed-orbit examples. At the relaxed first optimum, conservation itself limits the inner eccentricity to about 0.555. This is an implication at that value of s, not a global prior applied to all possible companions.

For the first fit, allowing an angular error of 0.1, 0.5, 1 or 2 degrees at each endpoint reduces the floors to 0.2447, 0.2202, 0.1892 and 0.1259 solar masses. With no normal error but endpoint eccentricity caps of 0.4, 0.6 and 0.8, they become 0.2347, 0.1986 and 0.1438 solar masses. These are sensitivity scenarios, not confidence limits. If endpoint eccentricities are also unconstrained near one, the floor can tend to zero. Total mass and mass ratio remain scenario inputs.

The code checks the torque inequality for 200,000 random orientations and eccentricities from zero to one. The largest exact-to-bound ratio is 0.999998744. Twelve independent secular integrations include outer response, initial eccentricities 0.05, 0.7 and 0.97, and s from 0.08 to 5. Every endpoint arc is below the sampled path length, which is below the torque budget. The largest invariant residual is below 7.6e-10. A separate random test checks the original capacity and torque conditions over masses, periods and outer eccentricities before elimination. All passing samples lie above the derived floor. These are implementation checks; the proof supplies the general result. Trajectories are synthetic and are not models of HD 93683.

## Limits and next tests

The result inherits the source eclipse model, fixed endpoint eccentricity and adopted 18+15 solar masses. We do not refit light curves or propagate their posterior. Linear-model values at epoch centers are not independent normal measurements. Sparse timing, third light, stellar surface models and branch ambiguity limit the evidence. The theorem does not need a physically constant drift, but it needs correct endpoint normal constraints.

At octupole order the outer angular momentum magnitude can change. Then the sphere in (3) has a changing radius and this proof does not apply. Short-period motion, failure of orbit averaging, stellar torques, mass loss and multiple perturbers also lie outside its scope. A model near the relaxed period has P2/P1 near ten, so its hierarchy and averaging must be checked rather than presumed. We establish neither a sharp bound nor a stable orbit that attains it. A joint light-curve and spectroscopic fit with full dynamics is still required to confirm a companion orbit. This work closes one assumption gap in a necessary test; it adds no observation.

## Reproduce and inspect

The package contains original code, narrative, figures, synthetic checks and aggregate calculations, plus an attributed baseline SCI input. No third-party raw data or restricted database is bundled. See `files/EXTERNAL_DATA_NOTICE.txt`. The shared dataset store was not used. The source archive is at `/mnt/dell-data/campaigns/11_07_2026/3bd1cefdd9df611df279a37839390d9414c980a8d15dd6f66103dee1fdc01627.zip`; its hashes are in `files/provenance.json`.

Use Python 3.12 with NumPy, SciPy and Matplotlib; exact tested versions are in `files/checks.json`. From a verified extracted bundle RESULT:

```
OPENBLAS_NUM_THREADS=1 python -B RESULT/files/analyze.py RESULT/files/inputs.json /absolute/path/to/new-output
python -B RESULT/files/retrieve.py /absolute/path/to/campaign /absolute/path/to/new-source-scratch
```

The first command recreates bounds.csv, checks.json and endpoint_bound.png offline. It runs in one process. The second verifies the cited SCI ZIP, recovers the aggregate input and records hashes in a new scratch directory. Compare the recovered input with the bundled input. Neither command writes into the signed package. No private scratch or network data download is needed. Environment version fields can differ.

Campaign 11_07_2026. Job sci-1107-dell-astronomy-12405b658a72. Topic astronomy. Machine dell. Account codex-myxtap. Model gpt-6.1-sol with high reasoning effort, through the Codex harness in T3 Code. Work date 2026-11-10. The signer is a campaign-machine identity, not a personal authorship claim.
