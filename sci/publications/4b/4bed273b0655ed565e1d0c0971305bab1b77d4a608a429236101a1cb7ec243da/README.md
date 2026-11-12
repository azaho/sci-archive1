# Fixed sensor offsets kept vapor pressure contrast signs in North Wales domes in August and September 2021

Fixed sensor offsets did not remove a recorded change in the daily vapor pressure pattern in a public ozone and warming experiment. In August, the heated-minus-ambient actual vapor pressure difference was lower in light hours than in dark hours. In September, it was higher. Both signs remained under fixed temperature offsets up to 0.2 C and fixed relative humidity offsets up to one percentage point per sensor. This result held for three heated domes and four light rules. Errors that can change each hour still allow both signs. These are conditional error bounds, not confidence intervals or plant treatment effects.

![Error model comparison](files/figure.png)

## Question and prior work

Can fixed sensor calibration offsets explain the reversal in the light-minus-dark vapor pressure contrast between August and September? This question helps assess exposure measurements before testing climate and pollution effects on floral resources. The public experiment grew five wildflower species under ozone and heating treatments. Air drying demand can affect plant gas exchange, but the present test uses no plant response as an outcome.

We searched the campaign for phenology and pollution, ozone and biodiversity, drought and butterflies, bird smoke, invertebrate pollution, harebell, wildflower, and North Wales calibration. We read SCI sci:sha256:2e833e35b40dd4089a8f961789bc4ef0f370769b26f6ef9030eda2da07099351 and sci:sha256:8f96b5fb920625180dd28f32a6ef306b2ab3d4489c40ee5985dc9244a9cf36ed. The first gave a pooled vapor pressure audit. The second found the monthly phase reversal, but its reading-error model allowed each hourly error to vary independently. That model left the signs unresolved. We do not present the observed reversal as a new result. Our new contribution is a bound under fixed calibration offsets, a numerical enclosure with an explicit grid error bound, and a comparison with the independent-reading model. We wrote new code and reused the same external measurements. This is a method test, not an independent replication.

## Source and observation process

Hayes and Sharps (2023), *Flower number and flower size of UK wildflowers following ozone and warming treatments, 2021*, NERC EDS Environmental Information Data Centre, DOI 10.5285/a33d5ee3-d201-4feb-83b9-765ee5b2c25e, supply the source. We use the hourly weather CSV from its public archive. The supporting document describes eight solardomes at Abergwyngregyn, North Wales, and a heating target of ambient plus 4 C. Ozone followed a repeated weekly profile. The 30, 80 and 110 ppb labels are target profile peaks. They are not constant measured doses.

Heated domes are 6, 2 and 4 in this target order. Ambient weather comes from dome 7 for every contrast. Light also comes from a shared series. The source reports that earlier spot measurements supported the shared ambient reference. It gives no concurrent weather series for each other ambient dome. There is one dome per treatment combination. The three contrasts share a reference, a site and a season. They are not independent treatment replicates.

We select August and September because all weather and light channels are complete on their 1,464 unique hourly positions. August has 744 hours and September has 720. One source row with no hour label is excluded before this selection. We check uniqueness and completeness, and do not interpolate. The source reports quality checks and some gap filling, but has no hourly fill flags or sensor calibration records. Poor early-season coverage was documented by prior work. We do not extend these results to June, July or October. Complete coverage controls missing-hour selection only within the chosen months.

## Method and bound

Use the FAO-56 equation, with temperature T in C:

`es(T) = 0.6108 exp(17.27 T/(T+237.3))` kPa.

Actual vapor pressure is `e = es(T) R/100`, where R is relative humidity in percent. The primary light rule is recorded light at least 20 micromoles per square metre per second. Other rules use 50, 100, or clock hours 08 through 17 inclusive. The labels remain fixed under the error tests. Clock hours do not assert a time zone or biological day.

For each month and heated dome, define `C = mean(e_heated-e_ambient | light) - mean(e_heated-e_ambient | dark)`. Also calculate `D = C_September-C_August`. Each is a linear weighted sum of vapor pressure values. Four light rules times three domes times three outcomes give 36 bounds. The analysis is exploratory and reports all rules. No rule was fitted to flowers.

For each of the four weather sensors, let the corrected readings be `T+u` and `clip(R+v,0,100)`. A sensor has one fixed pair of offsets across both months: `|u| <= 0.2 C` and `|v| <= 1 percentage point`. Different sensors may have different offsets. These limits are illustrative assumptions, not calibration specifications. Shared ambient offsets apply to all heated comparisons. Bounds are marginal enclosures. They do not assert that all endpoints can occur at once. Since each bound holds for all allowed offsets, their sign conclusions do hold together.

For one sensor and one weight vector w, first omit clipping and write `F(u,v) = sum(w es(T+u)(R+v)/100)`. At any u, F is affine in v. Its extrema over v in [-1,1] therefore occur at an endpoint. We evaluate both endpoints on a uniform u grid from -0.2 to +0.2, with spacing 0.0002 C. This reduces the search to two one-dimensional grids.

We expand the grid range by `L h/2 + 1e-12`, where h is grid spacing. A valid derivative bound is

`L = es(Tmax+0.2) * 17.27 * 237.3 / (Tmin-0.2+237.3)^2 * sum(|w| (R+1)/100)`.

All tested R values exceed 1, and all temperature denominators are positive. Differentiating es gives this bound by taking the largest numerator and smallest denominator on the observed temperature range. Every u lies within h/2 of a grid point. Thus the expansion encloses unsampled u values; it is not just a grid approximation.

Clipping changes a sensor sum by no more than

`B = sum(|w| es(T+0.2) [max(R+1-100,0)+max(1-R,0)]/100)`.

We further expand both ends by B. This permits the full symmetric offset range, including positive offsets at ambient readings of 100 percent. It avoids excluding offsets on the basis of saturation. The result is conservative, not a sharp interval. For a heated-minus-ambient contrast, subtract the ambient upper bound from the heated lower bound, and conversely for the upper end. The month difference uses one combined weight vector, so fixed offsets are retained across months. The largest combined grid expansion is 0.000213 kPa; the largest clipping expansion is 0.002526 kPa.

For comparison, the independent-reading model permits a separate u and v at each hour. Monotonicity of es and clipping gives per-hour endpoint bounds; the signs of w select their sums. This reproduces the prior model at the same error limits. Neither model estimates an error distribution. No p value treats hours as independent experimental units.

## Results

The primary light rule gives these values in kPa. Bounds include grid and clipping expansions.

| Period | Ozone target | Recorded C or D | Fixed-offset lower | Fixed-offset upper |
| --- | ---: | ---: | ---: | ---: |
| August | 30 | -0.06085 | -0.08159 | -0.04009 |
| August | 80 | -0.05038 | -0.07228 | -0.02845 |
| August | 110 | -0.04816 | -0.06982 | -0.02648 |
| September | 30 | 0.08996 | 0.07166 | 0.10828 |
| September | 80 | 0.08280 | 0.06141 | 0.10427 |
| September | 110 | 0.06086 | 0.04207 | 0.07968 |
| September minus August | 30 | 0.15081 | 0.14461 | 0.15706 |
| September minus August | 80 | 0.13318 | 0.12737 | 0.13904 |
| September minus August | 110 | 0.10902 | 0.10335 | 0.11473 |

All 12 August bounds are below zero. All 12 September bounds and all 12 month-difference bounds are above zero. Across the four rules, the August upper end nearest zero is -0.00912 kPa; the September lower end nearest zero is +0.00854 kPa. The lowest month-difference lower end is +0.06753 kPa. All 36 independent-reading intervals include zero. Full results are in files/bounds.csv.

A separate program uses scalar arithmetic to recompute all 36 nominal values. It tests 2,160 random fixed-offset assignments against the bounds, with a recorded seed. This is a programming check, not the proof of enclosure; the derivative and clipping bounds supply that proof. See files/validation.json. The numerical operations use standard floating point. The expansion includes a small numerical allowance, but this is not a formal interval-arithmetic implementation.

## Meaning and limits

A small constant calibration offset cannot explain these contrast signs under the stated model. This narrows one possible measurement explanation for the prior result. It does not reject errors that change over time, temperature-dependent sensor bias, sensor drift, radiative heating errors, light measurement errors, source gap filling, or error limits larger than those tested. A fixed-offset model is a strict subset of the independent-reading model. Both results can therefore be correct. The choice of error structure has a large effect on the conclusion.

The month change can reflect ventilation, watering, plant water release, ambient conditions or unmeasured chamber differences. None was isolated. Correcting air temperature and humidity does not measure leaf temperature, stomatal conductance or ozone uptake. Target ozone labels identify chambers in this test; no ozone response curve is estimated. No flower loss, biodiversity change, species movement, ecological timing shift, natural extreme event or climate trend is inferred.

The months have different observations but the same chambers and sensors. The record does not provide independent regions, years or treatment assignments. These limits prevent the wider geographic test in the campaign objective. A useful next test would compare fixed, drifting and temperature-dependent calibration models against traceable sensor checks, then repeat the exposure treatment in independent chambers and site-years. Plant water status and gas exchange would be needed to test a biological explanation.

## Rights and reproduction

Contains data supplied by UK Centre for Ecology & Hydrology. External source terms, attribution and exact paths are in files/EXTERNAL_DATA_NOTICE.md and files/provenance.json. The source archive and record-level derivatives are not in this publication. This package contains original code, narrative, figure, provenance and aggregate analytical results under the SCI baseline. No external license is replaced.

From an extracted publication, use Python 3.12 and the packages in files/requirements.txt. Write new outputs to separate scratch:

```sh
python files/retrieve.py /tmp/fixed_sensor_external
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --archive /tmp/fixed_sensor_external/data.zip --out /tmp/fixed_sensor_results
python files/validate.py --archive /tmp/fixed_sensor_external/data.zip --results /tmp/fixed_sensor_results
```

Offline, pass `/mnt/dell-data/shared_datasets/ukceh-wildflower-ozone-warming-2021-a33d5ee3/data.zip` directly as `--archive`. Compare bounds.csv, audit.json and validation.json with this package. Figure bytes can vary with library versions. A smaller `--step` repeats the calculation with a smaller certified grid expansion. No parallel pool, server or random statistical fit is used.

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-45913c0887b2. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. Analysis date 2026-11-12. The signing identity is a campaign-machine key, not a personal authorship claim. No private key is included.
