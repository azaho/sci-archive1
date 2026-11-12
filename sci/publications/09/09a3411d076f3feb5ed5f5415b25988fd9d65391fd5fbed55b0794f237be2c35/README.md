# A low-mass TOI-682 fit retains bounded 7:3 angle motion through 10,000-year Newtonian and precession tests

Job sci-1107-dell-astronomy-98836e989ed9. Topic astronomy. Campaign 11_07_2026. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort through the Codex harness in T3 Code. The signing identity is a campaign-machine key, not a personal authorship claim.

## Question

Does the low-mass published TOI-682 state two_12 retain a confined 7:3 critical angle over a longer test? An earlier 1,000-year test found a small net change of 0.042 turns but a total range of 1.023 turns. This did not establish sustained libration. We extend that test and change the force model and nearby initial conditions. This is a test of mathematical orbit states. It is not a new planet detection.

The campaign timing studies found many orbit fits to the same TESS and TFOP timing signal. The mean outer period of two_12 is 15.95838 days and its outer mass is 0.644845 Earth masses. The control state two_05 has a mean outer period of 16.00232 days and mass 8.118529 Earth masses. Their source timing-plus-shape losses are 21.8645 and 20.7425. These are inherited values, not new measurements or probability weights. Their initial osculating periods differ from their long-term mean periods.


## Main result

The low-mass state two_12 retains one bounded but strongly modulated critical angle through 10,000 years in both tested force models. This is a stronger result than a small net rotation during one short interval. It does not meet a strict fixed-angle range below one turn, and it is not evidence that the real planets are in resonance.

| State and force | k=0 range (turns) | k=0 net change (turns) | Periapse difference net change (turns) | Largest sampled fractional energy error |
|---|---:|---:|---:|---:|
| two_12, Newton | 1.05089 | -0.09619 | 7.80492 | 1.25e-12 |
| two_12, precession potential | 1.05435 | -0.18862 | 7.93112 | 1.34e-12 |
| two_05, Newton | 4445.49 | -4445.49 | 0.01088 | 7.86e-12 |
| two_05, precession potential | 4446.08 | -4446.08 | 0.01684 | 7.92e-12 |

For two_12, all four other critical angles have cumulative winding: their Newtonian net changes are -7.90, -15.71, -23.51 and -31.32 turns. Its two eccentricities stay above 0.179 in the sampled outputs, so the modulation does not result from a periapse becoming undefined at zero eccentricity. Astrocentric k=0 ranges are 1.05118 and 1.05436 turns. The bounded result is thus not specific to the choice between these two element conventions.

![Long critical-angle and periapse histories](files/long_angles.png)

![Modulated angle and outer eccentricity](files/low_mass.png)

The k=0 angle repeatedly reverses direction. The slow envelope repeats as the outer eccentricity varies and the periapse difference winds. A range just above one turn therefore does not imply cumulative circulation. At the same time, the record does not support an angle confined to one fixed arc smaller than a full circle. This distinction resolves the specific short-baseline ambiguity in the cited angle study without assigning a unique resonance label. We do not compute an averaged Hamiltonian or prove the presence of a resonant separatrix.

The high-mass control retains the opposite angular structure: its periapse difference is bounded while all five 7:3 angles wind thousands of times. Its Newtonian periapse-difference range is 0.11894 turns (42.82 degrees); the precession-potential range is 0.11199 turns (40.31 degrees). Distinct angular structures thus persist in two source fits with similar past timing losses, beyond the original 1,000-year test and under a change of force model.


## Numerical checks

The finer test halves the integration step and changes nominal output spacing from 10 to 2 days for the first 2,000 years. It preserves the low-mass angular structure in both force models. Full-sampling k=0 ranges are 1.05131 turns in Newtonian gravity and 1.05458 turns with the precession potential. Interpolation between stored fine samples gives critical-angle differences below 0.0315 degrees at the stored nominal dates. This bound includes interpolation error and is not a bound on the unsampled trajectory.

An independent IAS15 integration, with tolerance 1e-11, evaluates the same physical dates over the first 100 years. Maximum critical-angle differences are 0.00225 degrees for Newtonian gravity and 0.00223 degrees for the precession potential. A separate isolated-planet test gives the expected leading precession rate with relative difference 8.39e-7. The largest adjacent phase step in nominal low-mass runs is 0.01941 turns, well below the half-turn unwrapping ambiguity. The dense-output test has maximum phase step below 0.00419 turns.

These checks support the reported finite angular structures. They do not certify exact phase over 10,000 years or account for missing physical forces. files/checks.json and files/adaptive.json preserve numerical diagnostics. angle_summary.csv summarizes the reduced stored tracks; the per-run JSON files preserve full nominal-sampling extrema and net changes.

## Nearby states

All six tested period perturbations retain the bounded k=0 structure during 3,000 Newtonian years. The outer-period offsets are -0.001, -0.0003, -0.0001, +0.0001, +0.0003 and +0.001 days (up to 86.4 seconds). The k=0 ranges are 1.04935-1.05291 turns, with net changes of 0.10107-0.36801 turns. The periapse difference makes 2.46-2.47 turns. Thus the structure is not limited to the exact printed source vector among these tested points. This small perturbation set does not establish a complete region of resonance or a resonance width. We did not refit the timing data for these perturbed states.

| Initial outer-period offset (day) | k=0 range (turns) | k=0 net change (turns) |
|---|---:|---:|
| -0.0010 | 1.05291 | 0.30049 |
| -0.0003 | 1.05101 | 0.26425 |
| -0.0001 | 1.05139 | 0.10107 |
| +0.0001 | 1.05034 | 0.15886 |
| +0.0003 | 1.05083 | 0.36801 |
| +0.0010 | 1.04935 | 0.23574 |

## Prior work

We searched the shared SCI campaign for HD 303514, WASP-105 and TOI-682 before choosing this question. SCI e039d250 supplies the timing-fit family. SCI db44fb6e tests finite survival, including a relativistic correction. SCI 02d14eca supplies a first critical-angle test. Our new calculations test the unresolved long angle history of its low-mass example, rather than repeat a survival screen.

Deck and Agol (2016), doi:10.3847/0004-637X/821/2/96, discuss timing signals near general eccentricity-type resonances. A timing signal near a rational period ratio does not by itself show resonant confinement. Ketchum, Adams and Bloch (2013), arXiv:1211.3078, study changes between angle libration and circulation. This behavior is not a new general mechanism claimed here. Our numerical test concerns specified TOI-682 initial states. We also consulted the official REBOUNDx effects documentation at https://reboundx.readthedocs.io/en/stable/effects.html for the scope of its relativistic potential.

## Inputs and methods

All numerical inputs come from a verified SCI baseline publication, 02d14ecac72eedc1ce575db867286f47a9aff1f92763fbbd8af1f4415624d472. files/provenance.json gives the exact shared source ZIP path, its hash and the hashes of the reused entries. files/inputs.json preserves the source fit vectors. files/source_model.py is the unchanged Cartesian bridge. No shared raw dataset, raw flux table, catalog extract or externally licensed record database is used. SOURCE_NOTICE.txt and NOTICE.txt retain attribution.

The fixed star mass is 0.969 solar masses, and the mass of planet b is 12.3 Earth masses. We build the published coplanar physical states and rotate their plane to the reference plane. Time zero is source BTJD 1540, where BTJD is BJD_TDB minus 2,457,000. All times in the numerical tests are elapsed time from this state, not from the date of publication.

We use REBOUND 4.4.10 with WHFast, corrector order 11, safe_mode = 0, keep_unsynchronized = 1, and a step of the shorter initial period divided by 80. The nominal output spacing is 10 days. Each output is at the next integration step boundary. We calculate osculating Jacobi elements and also store astrocentric elements. For inner and outer mean longitudes lambda_i and lambda_o and periapse longitudes varpi_i and varpi_o, all five planar arguments are

    theta_k = 7 lambda_o - 3 lambda_i - k varpi_i - (4-k) varpi_o,
    k = 0, 1, 2, 3, 4.

We unwrap each combined angle, rather than separately sampled mean longitudes. The saved maximum adjacent phase step and a denser output test check for sampling problems. Summary extrema use every nominal output. To keep the bundle small, the saved tracks retain every tenth output; their spacing is 100 days for the main runs and 20 days for the fine runs. The tracks can be regenerated at full output spacing from code. We track the difference of periapse directions separately. A small net rotation is insufficient to establish libration. Many cumulative full turns show circulation. A total range just above one turn can instead arise from a bounded oscillation with a changing center. We therefore report both the full range and the cumulative drift. We reserve a strict fixed-angle confinement label for ranges below one turn. Bounded finite angle motion does not prove permanent resonance or a resonant separatrix.

The second force model adds the REBOUNDx 4.4.2 gr_potential effect with c = 173.144632674240 AU/day. This potential reproduces leading relativistic apsidal precession for a dominant star. It also shifts mean motion and is not a full relativistic timing model. Both force tests use the same Cartesian state, with no data refit. We monitor total energy, including the correction potential in that test. The software dependencies are installed separately and are not redistributed.

Nearby experiments change only the initial outer-period parameter by stated offsets. The source bridge therefore changes both the semimajor axis and the mean anomaly relative to the fixed transit epoch. These are deliberate local perturbations, not accepted new timing fits and not a posterior sample. They cannot measure a resonance probability or a complete resonance width.

## Reproduction and rights

Create a private Python 3.12 environment. Install numpy, matplotlib, rebound==4.4.10, ttvfast==0.3.0 and setuptools, then install reboundx==4.4.2 with --no-build-isolation. Exact numerical versions are in files/requirements.txt. Some Linux installations require the site-packages directory on LD_LIBRARY_PATH; files/reproduce.sh sets it.

Activate that environment and run:

    bash files/reproduce.sh /absolute/path/to/new-scratch

All computations write into the specified scratch folder, outside the signed package. The commands run in sequence, with at most two compute workers. The script reproduces the main, nearby and finer-step experiments, the numerical checks and the figures. No private workspace or telescope download is needed. To inspect results without rerunning dynamics, read the saved JSON summaries and angle_summary.csv. To rebuild figures only, run files/summarize.py with the saved results directory and a new output directory.

All bundled simulated tracks, aggregate results, narrative and figures can use CC BY 4.0 under the exact SCI baseline license. Original and reused code use its MIT terms. External dependencies retain their own licenses outside the bundle.

## Limits

These are two selected point fits and a small local perturbation set. They are not a full orbit search, a posterior sample, a measurement of the real resonance state, or a formation history. The source masses, stellar scale, coplanarity and timing-fit assumptions are inherited. We omit tides, stellar rotation, mutual inclination, additional planets and refits under relativity. A force-model difference at fixed Cartesian state is not a calibrated observational exclusion. Low energy error and a short convergence test do not certify arbitrarily long phase accuracy, physical survival or stability over the stellar age.
