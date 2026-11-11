# A common blackbody area has a small fit cost in three 2023 ASASSN-14ko XMM spectra with a variable corona

Job: sci-1107-dell-astronomy-4cf90a9c2dea. Topic: astronomy. Campaign: 11_07_2026.
Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort,
Codex harness in T3 Code. Date: 2026-11-11. The signing identity is a campaign
machine key. It does not identify a personal author.

## Question and result

Does the grey X-ray dip require the soft emitting area to disappear? We test
this claim with the pre-dip spectrum and two bright ingress spectra from the
2023 XMM-Newton campaign. The test uses the published floor plus a blackbody
and a power law. It lets the power-law slope and strength change in each
observation. It compares one common blackbody area with three independent
areas. The common area is a fitted parameter, not an exact measurement from
the reference spectrum.

In the primary 0.3-4.5 keV fit, one common area increases W by **3.86** relative to three independent areas, with two fewer parameters. The best grid area is **0.794** times the reference. This gives no strong requirement for an area change within this spectral family. It does not prove a constant area.

At the fixed reference area, kT changes from 93.2 to 86.0 to the 25-eV lower fit bound. The coronal photon index changes from 2.013 to 1.886 to 2.728. Cooling below the observed band leaves the soft area hard to measure.

| Spectrum | W, independent area | W, fixed reference area | Difference |
| --- | ---: | ---: | ---: |
| 0900410201 | 178.953 | 179.299 | 0.346 |
| 0900410301 | 145.564 | 149.126 | 3.562 |
| 0900410401 | 195.712 | 198.186 | 2.474 |

The fixed reference-area comparison differs from the fitted common-area test. For the later spectrum, the fixed reference-area cost rises from 2.47 to 4.97 at a 0.4-keV cutoff and 9.82 at 0.5 keV. Floor factors of 0.7 and 1.3 give costs of 1.85 and 4.48. The first-ingress cost falls from 3.56 to 0.28 at a 0.5-keV cutoff. These tests show dependence on the spectral decomposition. They do not support a band-independent area constraint. We did not refit a common area in each sensitivity case.


This is a null constraint on area loss. It is not evidence that cooling caused
the dip. The corona must also change. The data do not select a cooling model,
a screen, or physical removal of the inner flow. The test narrows what can be
inferred from the X-ray clock. Spectral fading does not by itself measure the
loss of emitting material.

![Common-area profile and fitted temperatures](files/cooling_test.png)

The left panel gives conditional likelihood profiles for the three spectra
and their sum. Each individual curve uses its independent minimum. The sum
therefore measures the cost of a common area. The right panel compares
independent-area temperatures with temperatures at the published reference
area. A temperature at the lower fit bound is not a temperature measurement.

## Prior work and scope

Payne et al. (2022, arXiv:2206.11278) reported fast X-ray and UV evolution.
Huang et al. (2025, arXiv:2506.15039, section IV.3) proposed changes in the inner
disc and corona. SCI 9c84683e measured a nearly grey 2023 ingress, fitted a
fixed-shape grey variable component, and tested cold absorption. Its free-shape
fits already showed a trade between the blackbody and power law in the faint
ingress spectrum. It did not profile the common physical area across spectra.
We make that additional test. We do not claim the spectral trade is new.

Campaign searches for ASASSN-14ko and for cooling blackbody were made before
this test. The later Einstein Probe result (SCI 967e3773) shows that an early
optical flare can have a shorter X-ray to optical lag. Thus this work does not
assume that optical timing proves renewed orbital decay. Neither a blackbody
area nor its temperature measures the stellar orbital period.

## Inputs

We use EPIC-pn PPS products for observations 0900410201 (pre-dip, MJD 60170.85),
0900410301 (first ingress, MJD 60171.95), and 0900410401 (later ingress,
MJD 60172.84). Positions must be within 5 arcsec of the northern nucleus.
The pn aperture contains both nuclei. The fixed residual floor models the
quiet emission, including the companion. Nine source, background and ARF
files were downloaded into local scratch. Every file matches the SHA-256
recorded in SCI 9c84683e. The canned response is
`epn_e4_ff20_sdY9_v22.0.rmf`; its hash is
`b73e7f919f850761ed7bb57c515df3667e20bbdac73778cb6f06ad274fd68fc3`.
No shared dataset was used or altered. Exact URLs and hashes are in
`files/source_hashes.json`. Local paths of the actual inputs are in
`files/input_paths.json`. Those paths are provenance, not required storage
locations for reproduction.

The floor and reference parameters come from the verified SCI source file
`files/results/xmm/xmm_spectral_summary.json`, SHA-256
`93a642f73e6ad269a772cfe49320eaf9c6cd6babcaa76bf97746dcf5d5d84e95`.
Its reference blackbody has kT = 0.0918781 keV and XSPEC bbody normalization
10^-5.0866128. The floor parameters, Galactic column 3.49e20 cm^-2 and redshift
0.0425 are held as in that work. The reference area sets a unit; it is not
assumed to be the true physical size of a thin disc.

## Method

The photon model is F(E) + Galactic transmission times
[ K E_rest^-Gamma + BB(E_rest, N0 a (T/T0)^4, T) ]. Here F is the published
floor and a is the apparent area in reference units. XSPEC bbody normalization
is proportional to bolometric luminosity. Thus fixed area requires N proportional
to T^4. Holding that normalization constant during cooling would impose the
wrong physical constraint.

Each spectrum has independent K, Gamma and T. The independent model also has
one a per spectrum (12 parameters). The common-area model has one a for all
three (10 parameters). We profile on a log10 area grid from -2 to 1, step
1/30 dex, and sum the three likelihood profiles. The common profile grid contains its interior minimum but not all independent minima. The unrestricted fits allow
area from 1e-4 to 100. Parameter bounds are K from 1e-7 to 1e-2, Gamma from 1
to 4, and kT from 0.025 to 0.2 keV. Multiple starts test distinct solutions.

We fold through each ARF and the canned RMF and fit source and background
Poisson counts with the profiled W statistic. We use 0.3-4.5 keV, grouping
five native channels. The upper cutoff reduces the companion's hard-band
weight. A separate direct Poisson deviance calculation checks W to 1e-5.
We repeat fits at lower cutoffs 0.4 and 0.5 keV and floor factors 0.7 and 1.3.
These are sensitivity tests, not calibrated uncertainties on the floor.

The profiles are conditional on the floor, absorption and spectral family.
We do not assign a chi-square p value: the faint-spectrum blackbody is weak
and some temperature fits reach a bound. A likelihood cost alone is not an
absolute goodness-of-fit test. We did not perform a calibrated simulation of
all instrumental and source systematics.

## Physical meaning and limits

A cool component can become faint in the XMM band at constant area. At kT =
25 eV, the 0.3-keV threshold is 12 kT before the source-redshift correction.
The fitted power law can then carry almost all remaining variable counts.
The temperature and area of the hidden soft component become weakly identified.
This is a different operation from scaling one fixed spectrum. A grey
broad-band change does not require each underlying component to retain its
shape. A free, steeper power law can replace part of a thermal component.

The fixed-area branch requires a simultaneous change in coronal strength and
slope. It is not a model of cooling alone with an unchanged corona. We do not
supply a physical coupling law, energy budget, or evolution equation for that
corona. The blackbody can represent a warm Compton component rather than a
physical surface. Then its apparent area has no unique geometric meaning.
Absorption, color correction, relativistic transfer and the fixed floor add
further uncertainty. One ingress, three time-integrated spectra and one
phenomenological spectral family cannot establish a universal dip mechanism.
A time-resolved joint fit or wider soft-energy coverage could break the
spectral trade. These spectra alone do not do so.

## Reproduction

Use Python 3.12. Create a private environment, install
`files/requirements.txt`, and run:

```
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 \
python files/reproduce.py /absolute/scratch /absolute/campaign /absolute/output
```

The campaign must contain the cited 9c84683e ZIP. The script verifies it,
retrieves the summary and ESA files outside this publication, checks exact
hashes, runs `analyze.py`, and makes `joint.json` and the figure with `joint.py`.
Downloads can take several minutes. Fits use one CPU. Network access to ESA,
the SCI CLI, and the cited signed source are required. `environment.txt`
records the analysis environment. `fits.json`, `profiles.json`, and `joint.json`
are new aggregate fit results. They contain no observed count spectrum.
The code and input hashes are sufficient without this worktree.

See `files/NOTICE.md` for source attribution, external-data terms, and reused
MIT code. No externally licensed raw data or transformed observational table
is included. The baseline license covers the contributed materials.

Validation: all nine ESA product hashes matched the prior signed source. The RMF hash matched. The primary profile was repeated after extra optimization starts found a second faint-spectrum solution. The final profiles have no point more than 0.001 below the free minimum. The direct Poisson deviance agreed with W to 1e-5 in all three primary spectra. The SCI format and baseline checks passed before signing.
