# A 200 K BT-Settl surface contrast fits eight optical dip depths of TIC 262400835 with dust opacity index 2

Job: sci-1107-hp-astronomy-06cd0251b7f6. Topic: astronomy.
Campaign: 11_07_2026. Machine: hp. Account: codex-olen.
Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code.
Date: 2026-11-11. One worker did this study. No agents were launched.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

The optical dip colors of TIC 262400835 do not require a dust opacity index above 2
when the occulted and unocculted stellar light have different spectra. We give a
specific model that fits eight published ground-based depths from two nights.
The surface has projected area fractions 2/3 at 3000 K and 1/3 at 3200 K. Dust
covers part of the cool component. Both nights use the same surface mixture and
opacity law, kappa proportional to wavelength^-2. The dust columns change between
nights. The fit has chi-square 4.8875 for eight depths and five fitted screen
values. Every residual is below 1.60 stated marginal errors. The score uses the
quoted errors as diagonal weights; it is not a test that detects this surface map.

The model uses BT-Settl CIFIST2011 spectra and the total MuSCAT2 response. A second
fit at log(g)=4.0 keeps all residuals below 1.89 errors, but needs a much larger
covered area on the first night. Thus the color construction survives one gravity
change, while its inferred cloud area depends strongly on the atmosphere model.

We also strengthen the earlier single-spectrum test. With the filter integral
inside the extinction model, the linear combination

    0.27 D_g - D_r + 0.73 D_i <= 0

holds for every nonnegative dust column mixture with opacity index 0 to 2 in each
of 36 tested response and spectrum models. The 15 December depths violate this
bound by 0.4581 percentage points, or 3.734 stated standard errors under independent
Gaussian errors. Unknown cross-band covariance lowers the statistic to 2.303.
The earlier rejection therefore survives band integration within this tested set,
but its shared stellar color assumption matters.

![Band-integrated screen test and constructed surface model](files/screen_test.png)

The new result is a continuous-column bandpass test and a data-based example that
breaks its common-color assumption with a 200 K surface contrast. It does not
identify a dust composition, measure a stellar surface map, or solve the supply
and life of the corotating material. Those questions need additional constraints.

## Question and prior work

The selected SCI work concerns sharp dips in young, rapidly rotating M dwarfs.
Their age dependence and long recurrence do not identify what blocks the light.
[Bouma et al. (2026)](https://arxiv.org/html/2609.00136v1) give optical and infrared
dip depths and favor dusty plasma. Their Table 4 gives the measurements used here.

SCI c54e34ee (full ID in sci.json)
found that one optical color combination fails a general patchy screen with an
opacity index at most 2. It used nominal wavelengths. It left full filter
integration and stellar color differences as open checks. SCI 873546b7 shows why
free columns can hide larger opacity indices. This makes the assumptions behind
a claimed lower index bound important.

The effect of different occulted and mean stellar spectra is established in
planet transit work; see [Rackham, Apai and Giampapa (2018)](https://doi.org/10.3847/1538-4357/aaa08c).
We do not claim that effect as new. We apply it to the specific CPV residual with
physical atmosphere spectra, band integration, positive cloud areas, and one fixed
surface across two nights. We also give an optical-depth certificate that does
not rely on a sampled grid of cloud columns.

We searched the campaign for CPVs, gas opacity, phase memory, radiative cores,
bandpasses and stellar surface contrast before this test. Many recent results
already test phase motion, host recurrence and magnetic trapping. We read published
results only. We chose this scope after inspection of the released table. This is
an exploratory model check, not a preregistered population discovery.

## Inputs and rights

We use only the four simultaneous ground-based depths on each of 13 and 15 December
2020 in Table 4 of arXiv:2609.00136v1. These are the two MuSCAT2 nights for
TIC 262400835. We omit the TESS depths that the source paper flags for exclusion.
We omit the third night because it used MuSCAT1 and had no i-band depth. We do not
refit photometry or add observations.

The responses come from Figure 7 on PDF page 7 of
[Narita et al. (2019), arXiv:1807.01908v2](https://arxiv.org/html/1807.01908).
The figure includes the instrument optics and detector efficiency. The responses
are digitized from the original 576 by 432 pixel plot, not from a screenshot of a
web page. The four spectra at log(g)=4.5 have temperatures 2800, 3000, 3200 and
3400 K. The two spectra at log(g)=4.0 have temperatures 3000 and 3200 K. All have
solar abundance and come from the SVO BT-Settl CIFIST2011 service. See
[Allard, Homeier and Freytag (2012)](https://doi.org/10.1098/rsta.2011.0269).

[files/input_manifest.json](files/input_manifest.json) gives exact source URLs,
versions, byte sizes, SHA-256 hashes and shared paths for all eight input files.
Shared paths start with `/mnt/dell-data/shared_datasets/`, the HP SSD compatibility
path behind `./datasets`. We reused the four log(g)=4.5 spectra and the CPV article
in place. The campaign dataset helper added the instrument PDF and the two
log(g)=4.0 spectra. Existing datasets were not changed.

All raw articles, spectra, extracted responses, binned spectral fluxes and source
depth tables remain outside this publication. The package contains original code,
text, a figure and scientific fit or certificate results. Source terms and credit
are in [files/NOTICE.txt](files/NOTICE.txt). The exact SCI baseline license applies
to the bundled original material. It does not relicense the external inputs.

## Method

We measure dust optical depth at 750 nm. For photon response R_j and energy spectrum
S, the normalized wavelength weight is proportional to lambda R_j S. Each column
kernel is the weighted integral of 1-exp[-tau (750/lambda)^2]. Integrating that
kernel over any nonnegative column measure gives the band depth. The measure has
total area at most one. Extinction, a fixed baseline and common stellar color are
assumed for the certificate. Scattered light, cloud emission, limb darkening and
companion dilution are outside that null model.

We extract the two plotted response figures with the separate Poppler `pdfimages`
command. Exact RGB line pixels give a mean curve position for each image column.
Six x ticks, at image pixels 95, 171, 247, 322, 398 and 474, map to 400 through
900 nm. Image rows 52 and 378 give transmission 1 and 0. We use zero response
outside each traced curve. The figure is a finite-resolution calibration source.
The chosen independent +/-2 nm shifts of the four bands are stress tests, not
measured instrument uncertainties. Atmospheric transmission and nightly response
changes are not measured here.

Fine spectral lines are integrated before the spectrum is reduced to 0.1 nm
bins. A repeat at 0.2 nm checks that reduction. The certificate uses four single
spectra and, for each, the nominal response plus all eight independent g,r,i
shift combinations. Its coefficient is fixed across these 36 models. A small-tau
Taylor bound, monotone exponential bounds on a finite interval, and an analytic
large-tau bound cover every nonnegative optical depth. The calculation uses double
precision; it is not an outward-rounded interval proof of physical filter curves.
The explicit bounds, finite-model scope and smaller-index extension are given in
[files/method.md](files/method.md).

For the two-temperature construction, the band depth is multiplied by the fraction
of total band light from the cool component. This factor changes with band because
the two atmosphere spectra differ. Only the cool component is occulted. On the
first night we fit a moderate column and an opaque column with fixed tau=60. On
the second night we fit one column. The five free values are three covered areas
and two optical depths. All areas are nonnegative and fit inside the cool surface.
The stellar temperatures, their area ratio and the opacity index stay fixed.
The model flux spectra serve as isotropic surface-brightness templates.

We also solve a linear program with 502 column kernels. It minimizes the largest
absolute residual in units of the quoted error and enforces the total area bound.
This produces explicit finite feasible screens. It does not prove a continuum
minimum. Controls use one 3000 K spectrum, or two Planck spectra with the same
3000/3200 K temperatures and 2:1 area ratio.

## Numerical results

The main fit uses log(g)=4.5. Areas in this table are fractions of the cool area.

| Night | Moderate column tau at 750 nm | Moderate covered area | Opaque covered area | Largest residual / stated error |
|---|---:|---:|---:|---:|
| 13 December | 0.153126 | 0.148504 | 0.0300333 | 0.136 |
| 15 December | 0.729495 | 0.127930 | 0 | 1.600 |

The opaque column has tau=60. Total covered areas over the whole stellar disk are
0.1190 and 0.0853. The two night scores are 0.0436 and 4.8439, with total chi-square
4.8875. The model's area-weighted bolometric temperature is 3071.07 K. The source
paper gives an SED temperature of 3074 K for this object. This numerical proximity
is not an independent fit to its SED or a constraint on the surface map.

| Fixed source-light model | Finite-screen maximum residual, 13 December | Finite-screen maximum residual, 15 December |
|---|---:|---:|
| Single 3000 K atmosphere | 1.897 | 2.630 |
| 3000/3200 K Planck spectra, 2:1 areas | 1.936 | 2.662 |
| 3000/3200 K BT-Settl spectra, 2:1 areas | 0.113 | 1.370 |

These are numerical minima on the specified column grid. The last row supplies
explicit feasible screens with every depth within 1.370 errors. Their columns and
positive areas are in `files/results/results.json`. The main five-value fit above
has a simpler column structure and is the reported chi-square fit. The two
objectives have different optimum residuals.

The Planck control shows that the result depends on structure in the adopted
atmosphere spectra. In the two-temperature atmosphere model, the cool-light
fraction has an r/g ratio of about 0.959 and an i/r ratio of about 1.265. A smooth
continuum color correction does not reproduce that shape. We do not identify a
specific molecule or establish that the library has no spectral errors.

For the single-spectrum certificate, the gaps on 13 and 15 December are 0.3674 and
0.4581 percentage points. Independent-error statistics are 2.976 and 3.734. Reusing
the earlier conservative family size of 24 gives probability bounds of 0.0351 and
0.00226 under that Gaussian model. The largest error allowed by the stated
marginal errors gives statistics 1.815 and 2.303. Thus unknown covariance still
prevents a covariance-independent 5% rejection with that correction.

## Checks and limits

Changing from 0.1 to 0.2 nm bins changes the main chi-square by less than 0.0003 and
the largest standardized residual by less than 0.00004. All 36 continuous-column
certificates close; at most 364 finite intervals are needed per model. The least
negative interval upper bound is about -2.9e-7 in kernel depth units. One thousand
synthetic nonnegative column mixtures pass the nominal certificate.

Refitting the five screen values at all 16 independent +/-2 nm shifts of the four
response curves gives chi-square 4.52 to 5.27 and largest residual 1.55 to 1.65.
Using the filter-only Figure 6 response in place of the total instrument response
gives chi-square 4.65 and largest residual 1.56. These chosen perturbations do not
cover every real throughput, telluric or calibration error.

At log(g)=4.0, the same temperatures, area fractions and dust index give chi-square
7.26 and largest residual 1.89. The first night needs the full cool area covered,
or 2/3 of the whole projected disk, mostly at tau about 0.016. At log(g)=4.5 only
about 12% of the disk is covered. Colors alone therefore give a poor cloud-area
constraint in this model. We have not checked a wider gravity or abundance grid.
The published single-star radius and mass would suggest lower gravity; unresolved
multiplicity can bias those values. The gravity check is material to the scope.

The two-temperature surface was chosen after exploratory model checks. Five
screen values are fitted to eight depths. There is no independent validation of
the temperatures, surface fractions, selective coverage of the cool component,
cloud geometry or model spectrum. The fitted areas are projected-area values in
a model without limb darkening. A spatial surface map, a transit duration model,
a coeval binary model and a joint fit to rotational variability are not supplied.

The source depth fits share some timing and shape choices across bands, and no
full depth covariance is available. We have not remeasured the baselines or the
raw photometry. The chi-square values are descriptive, and we give no formal
preference probability between surface models. The fit does not measure a dust
index, grain size, mass, supply rate, magnetic field or lifetime.

A direct test is to measure simultaneous in-dip and out-of-dip spectra through
stellar molecular bands and continuum regions. The constructed surface gives one
common spectral-light factor for both nights, while the dust-column factor changes.
Joint modeling of that factor, the rotational light curve and the SED can test
whether this color construction is physically allowed for the star.

## Reproduction

Use Python 3.12 with numpy, scipy, matplotlib, Pillow and beautifulsoup4, plus the
separate Poppler `pdfimages` executable. The recorded run used Python 3.12.15,
numpy 2.5.4, scipy 1.18.1, matplotlib 3.11.2 and Poppler 26.01.0. Use one numerical
thread. The pipeline runs one process at a time and needs no service.

From the extracted publication root, with the campaign dataset path:

```sh
sh files/code/run.sh /mnt/dell-data/shared_datasets /absolute/path/to/separate-scratch
```

If the shared inputs are unavailable, retrieve them outside the publication first:

```sh
python files/code/retrieve.py /absolute/path/to/external-inputs
sh files/code/run.sh /absolute/path/to/external-inputs /absolute/path/to/separate-scratch
```

Retrieval checks every stated SHA-256. A changed online rendering or spectrum is
an error, not a new silent source version. The scripts refuse to write generated
outputs inside this publication. They regenerate extracted responses, depth tables
and binned spectra only in separate scratch. Compare the JSON numbers with
`files/results/`; PNG bytes can differ with rendering software.

`files/provenance/reproduction_check.json` records the fine/coarse comparison and
source-code hashes. The result package keeps all production code, source retrieval
instructions, input provenance, fit values, numerical certificate evidence and the
figure. Reproduction does not depend on this worker's private scratch.
