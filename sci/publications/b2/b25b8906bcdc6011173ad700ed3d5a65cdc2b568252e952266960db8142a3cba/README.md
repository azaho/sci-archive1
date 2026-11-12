# One-point humidity offsets permitted both August water-vapor signs but kept six drying-demand contrasts positive in North Wales in 2021

In a public ozone and warming experiment, assumed relative humidity offsets of up to one percentage point per sensor permit both signs of the mean heated-minus-ambient actual vapor pressure in August. The same error model keeps all six monthly air vapor pressure deficit (VPD) contrasts above zero in August and September. Temperatures are held at their released values. These are exact conditional measurement bounds, not measured sensor errors or confidence intervals.

![Humidity offset bounds](files/sensor_bounds.png)

## Question and advance

Can small humidity offsets change the conclusion that heated air had less actual water vapor, while leaving its higher drying demand clear? The distinction matters before using air conditions to explain flower responses to ozone and heat. VPD describes atmospheric demand; actual vapor pressure describes a different air property. Neither measures leaf ozone uptake.

Campaign searches used “phenology pollution”, “climate biodiversity”, “ozone”, “wildflower ozone”, “vapor decomposition” and “humidity vapor”. We read the following signed results:

* sci:sha256:2e833e35b40dd4089a8f961789bc4ef0f370769b26f6ef9030eda2da07099351 gave higher VPD and a small negative actual vapor contrast in August-September. It did not give the humidity offset needed to remove those mean signs.
* sci:sha256:4bed273b0655ed565e1d0c0971305bab1b77d4a608a429236101a1cb7ec243da bounded light-minus-dark actual vapor contrasts under fixed temperature and humidity offsets. Its outcome has signed weights across light classes. Our outcome is the all-hour monthly mean. These tests answer different questions.
* sci:sha256:2b9508d6586c4ab7fc5b43479386ba62f0df6c42c4718cecabf1b5e9067993ec tested ozone rankings under common VPD response weights. It shows why atmospheric exposure does not directly establish uptake.

Our new test compares the exact humidity error thresholds for two mean air properties. It uses the same records and new code. It is an exploratory measurement follow-up, not independent regional or yearly validation. The wider biological and geographic objective remains open.

## Source and observation process

Hayes, F.; Sharps, K. (2023). *Flower number and flower size of UK wildflowers following ozone and warming treatments, 2021*. NERC EDS Environmental Information Data Centre. DOI: 10.5285/a33d5ee3-d201-4feb-83b9-765ee5b2c25e.

The experiment was at Abergwyngregyn, North Wales. Heated domes 6, 2 and 4 had nominal ozone peak targets of 30, 80 and 110 ppb. Heating was nominally ambient plus 4 C. The targets describe weekly profiles, not constant ozone concentrations. One ambient weather series from dome 7 is used in all comparisons. The source cites earlier spot checks to support that choice. Concurrent weather in the other ambient domes is not available.

We select August and September because every temperature and humidity channel is present for all 744 and 720 unique hourly positions. No values are interpolated by us. The source reports quality control and some gap filling, but gives no fill flags or sensor calibration estimates. Complete coverage does not establish that all values are direct, accurate readings. Earlier months have major weather gaps. October has no flower visits. We do not extend the primary test to them.

Each treatment combination has one dome at one site in one year. Pots and hours are not independent treatment assignments. Both months use the same sensors and domes. We analyze no flower response and make no causal claim about warming, ozone or biodiversity.

## Exact bound

For temperature T in C and relative humidity R in percent, use the FAO-56 saturation pressure formula:

`S(T) = 0.6108 exp(17.27 T/(T+237.3))` kPa.

Actual vapor pressure is `e = S(T) R/100`; VPD is `v = S(T) - e`. The transform of hourly means need not equal a mean computed from finer readings.

Let each sensor have one constant RH correction u over a month, with `-b <= u <= b` percentage points. Heated and ambient corrections can differ. Use `clip(R+u,0,100)` and hold temperatures fixed. We allow clipping at saturation rather than exclude possible offsets on the basis of recorded RH. These limits are assumed, not instrument specifications.

The mean actual vapor contrast is monotone increasing in heated u and decreasing in ambient u. Thus its sharp lower bound is

`L_e(b) = mean[S_h clip(R_h-b)/100 - S_a clip(R_a+b)/100]`.

Its sharp upper bound `U_e(b)` uses +b for heated RH and -b for ambient RH. Here clip has limits 0 and 100. Both endpoints are attained by constant sensor offsets. Put `D_S = mean(S_h-S_a)`. The exact VPD bounds are `[D_S-U_e(b), D_S-L_e(b)]`. No search over hourly errors is needed. If errors can change independently each hour with the same limits, the bounds for these means are unchanged: every term has the same direction in its own sensor. This property does not apply to the prior light-minus-dark outcome.

All observed e contrasts are negative. We solve `U_e(b)=0` for the smallest error allowance that permits zero. For VPD we solve `D_S-U_e(b)=0`. Continuous monotone endpoints give these thresholds; numerical root residuals were below 1e-10 kPa. Values beyond the threshold permit a sign reversal. Bounds are marginal for each month and dome. A common ambient correction cannot generally attain opposite endpoints for different outcomes at once. However, a sign that holds for every correction holds jointly across the comparisons, including if offsets must stay fixed across both months.

## Results

| Month | Ozone peak target, ppb | Recorded e contrast, kPa | e bounds at b=1, kPa | RH threshold for zero e, points | RH threshold for zero VPD, points |
| --- | ---: | ---: | ---: | ---: | ---: |
| August | 30 | -0.04229 | -0.10016 to +0.01613 | 0.72389 | 15.35509 |
| August | 80 | -0.04468 | -0.10195 to +0.01314 | 0.77278 | 14.52113 |
| August | 110 | -0.01777 | -0.07419 to +0.03921 | 0.31182 | 12.77462 |
| September | 30 | -0.08576 | -0.14171 to -0.02917 | 1.51557 | 14.25445 |
| September | 80 | -0.08027 | -0.13775 to -0.02215 | 1.38120 | 16.41920 |
| September | 110 | -0.09298 | -0.14771 to -0.03760 | 1.67904 | 12.50484 |

Contrasts are heated minus the shared ambient reference. At a one-point bound, August actual vapor signs are unresolved. September actual vapor remains lower under this error model. It first permits zero at 1.38-1.68 points. Across the six tests, VPD lower bounds at one point range from +0.63707 to +0.89615 kPa. Its sign requires allowances of 12.50-16.42 points to reach zero with temperatures fixed. These large thresholds are sensitivity diagnostics, not plausible-error estimates. No threshold was selected to fit flowers.

A scalar implementation independently recomputed all 12 one-point endpoints. Six actual vapor roots and six VPD roots passed residual checks. Full precision is in files/sensor_bounds.csv and checks are in files/validation.json. Floating-point bounds are not formal interval arithmetic proofs. The monotonicity argument supplies the bound logic. We report no hour-based p value or sampling confidence interval.

## Meaning and limits

A clear VPD difference does not establish a similarly secure actual water-vapor difference. Humidity calibration that is adequate for one air property can be inadequate for another. The August result does not refute the recorded negative means; it shows how small opposing sensor offsets could remove their signs. September gives a different conditional result in the same season. No calibration data were found to assign probabilities to the permitted offsets.

Temperature error, drift, temperature-dependent RH bias, radiation error and an incorrect shared ambient reference remain outside this model. The threshold comparison can change if temperatures are uncertain. Actual vapor pressure is not water mass per unit volume or specific humidity; changing temperature and pressure matters for those conversions. We do not infer water removal, plant transpiration, stomatal conductance or absorbed ozone from these contrasts. A lower RH is not itself proof of less actual vapor.

The data cannot separate direct heat effects, drying demand, chamber conditions and plant state. Independent regions, years and treatment replicates were not tested. A next study should first obtain traceable temperature and humidity checks in every dome, retain fill flags, and test the mean contrasts jointly under those error limits. Replicated humidity-controlled warming experiments with soil water, leaf temperature, conductance and flower observations could then test biological explanations.

## Reproduction and rights

Contains data supplied by UK Centre for Ecology & Hydrology.

The source uses Open Government Licence v3. Raw data, documents and record-level derivatives remain outside this publication. Only original code, narrative, figure, provenance and six aggregate analytical results are bundled under the SCI baseline. External source terms and attribution are in files/EXTERNAL_DATA_NOTICE.md. Exact URLs, used member hashes, shared path, version and software versions are in files/provenance.json.

From an extracted package, with Python 3.12 and packages in files/requirements.txt:

```sh
python files/retrieve.py /absolute/path/to/new_external_scratch
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/sensitivity.py --source /absolute/path/to/new_external_scratch/data.zip --out /absolute/path/to/new_results
```

On this campaign machine, reuse `/mnt/dell-data/shared_datasets/ukceh-wildflower-ozone-warming-2021-a33d5ee3/data.zip` as --source and skip retrieval. Write outputs outside the signed package. Compare sensor_bounds.csv and validation.json with the bundled versions. Image bytes can vary with library versions. No private scratch is needed. A changed ZIP wrapper requires source inspection before changing the asserted archive hash; the exact scientific member hash is recorded.

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-aaa8f08d8e80. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. Analysis date 2026-11-12. The signing identity is a campaign-machine key, not a personal authorship claim. No private key is included.
