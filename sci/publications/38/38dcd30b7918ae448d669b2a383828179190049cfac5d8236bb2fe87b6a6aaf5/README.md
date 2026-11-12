# Separate response scales permitted ozone ranking reversals in North Wales domes in August-September 2021

A shared dry-air response does not guarantee an ozone exposure ranking when its scale differs between heated and ambient plants. In four high-target month comparisons, a heated response multiplier above 1.0132 to 1.0503 first permits a positive weighted concentration contrast. These small limits apply to the most permissive common response shapes. Tested smooth shapes need much larger multipliers. These are exact sensitivity limits for fixed readings. They are not estimates of conductance, ozone uptake or flower injury.

![Scale sensitivity](files/scale.png)

## Question and new contribution

Does the earlier shared-response ranking survive a difference in response scale? This matters for studies of warming, air pollution and flowers. Plant acclimation or ozone injury can change how much gas passes through leaf pores even at the same air drying demand.

We searched the campaign with `phenology`, `pollution biodiversity`, `drought birds`, `solardomes` and `VPD separate`. We read three related publications. SCI sha256:2e833e35b40dd4089a8f961789bc4ef0f370769b26f6ef9030eda2da07099351 found higher air vapor pressure deficit (VPD) in heated domes. SCI sha256:2b9508d6586c4ab7fc5b43479386ba62f0df6c42c4718cecabf1b5e9067993ec proved that every common non-increasing VPD response gave a nonpositive heated-minus-ambient ozone summary in August and September. It left unequal chamber responses open. SCI sha256:9d90934a275052dd457cb0d880d074ee7b4b41f8be11e913cbd4cde77aeebb6b allowed a joint light and VPD response. Its small August concentration reversals each selected one hour.

Our new test keeps a common VPD response shape but permits a uniform relative scale difference. It gives the exact scale threshold, checks simple smooth shapes, and tests removal of the brightest hour. We rebuilt from source and used no earlier code. These are the same chambers and records. This is not independent regional or yearly validation and does not refute the earlier shared-scale theorem.

Emmerichs et al. (2025), DOI 10.5194/bg-22-4823-2025, compared ozone deposition models whose results depend on environmental and plant response assumptions. That work motivates a response sensitivity test. It does not supply calibration for our multiplier. We do not fit a deposition model.

## Data and observation limits

Hayes, F.; Sharps, K. (2023). Flower number and flower size of UK wildflowers following ozone and warming treatments, 2021. NERC EDS Environmental Information Data Centre. DOI: 10.5285/a33d5ee3-d201-4feb-83b9-765ee5b2c25e. Release date: 2023-12-20.

The experiment was at Abergwyngregyn, North Wales. Weekly ozone peak targets were 30, 80 and 110 ppb in the paired comparisons. Heated/ambient dome pairs were 6/3, 2/1 and 4/5. Heating targeted ambient plus 4 C. There was one dome per treatment combination. Ambient temperature and humidity came from dome 7 for every ambient ozone dome. Separate local ambient measurements were not available. Earlier spot checks do not establish exact equality during these records.

August and September have 744 and 720 complete unique hourly labels. We use these months because early summer weather is incomplete. October has no flower observation month. We do not fill gaps or use flower outcomes to select records. The primary light rule is measured photon flux above 50 micromoles per square metre per second. It keeps 380 August hours and 317 September hours. Other rules use all hours, light above 10, light above 100, and light above 50 with the brightest hour omitted. Each rule selects the same hours in both chambers. No time zone is inferred.

The provider reports quality control and possible gap filling but supplies no hourly fill flags or calibration error estimates. VPD calculated from hourly mean temperature and humidity can differ from mean VPD at finer resolution. Shared ambient weather, changing sensor errors and chamber differences remain limits. Hours are not independent treatment replicates. The two months share plants, chambers and sensors.

## Method and proof

Calculate VPD in kPa as `V = 0.6108 exp(17.27 T/(T+237.3)) (1-RH/100)`, using T in C and RH in percent. The saturation pressure formula follows FAO guidance.

For n selected hours, H and A denote heated and ambient ozone. Let f be a common response shape that takes values in [0,1] and never increases with VPD. Let r >= 1 be a uniform heated relative response multiplier. Define

`D_r(f) = mean[r aH f(VH) - aA f(VA)]`.

The main a is ozone concentration in ppb. A separate diagnostic uses `a=max(ozone-40,0)`. The denominator stays n, not the sum of weights. This is a relative weighted concentration summary, not AOT40 or absorbed dose. If final responses must be at most one, scale f down uniformly by r. This leaves every contrast sign and threshold unchanged. Plotted magnitudes use the ambient response scale, not a measured physical flux scale.

Pool the distinct observed VPD values v_i. Let H_i and A_i be cumulative heated and ambient ozone sums up to v_i, divided by n. Any non-increasing f on this finite support is a nonnegative mixture of step functions `1[V<=v_i]`, plus the zero function. Thus

`U(r) = max_f D_r(f) = max(0, max_i [r H_i - A_i])`.

If any H_i is positive, define `r_star = min_{i:H_i>0} A_i/H_i`. Then no positive contrast is possible at r <= r_star. A positive contrast is possible at every r > r_star, attained by a minimizing step. Equality gives zero, not a positive reversal. This is an existence threshold; it does not make every response positive. The zero response always gives zero. If heated and ambient a are both zero, reversal is impossible for any finite r.

This finite-support ratio calculation is a direct extension of the earlier cumulative-sum test, not a new general optimization theorem. We also solve a fractional linear problem in another form: minimize A(f), subject to H(f)=1, f nonnegative and non-increasing. No upper scale bound is needed because the ratio is unchanged by scaling. This supplies a second numerical algorithm for the threshold.

We tested smooth shapes `f(V)=exp(-V/S)` for S of 0.5, 1 and 2 kPa, using the primary light rule and concentration. Their exact scale threshold is `sum[aA f(VA)]/sum[aH f(VH)]`. These examples are not calibrated plant response curves. The analysis is exploratory and has no probability intervals or hourly significance tests.

## Results

Primary concentration thresholds are:

| Month | Peak target ppb | Critical multiplier | Increase at equality | Heated / ambient hours in witness |
| --- | ---: | ---: | ---: | ---: |
| August | 30 | 1.169879 | 16.99% | 380 / 380 |
| August | 80 | 1.013203 | 1.32% | 380 / 380 |
| August | 110 | 1.013935 | 1.39% | 380 / 380 |
| September | 30 | 1.213611 | 21.36% | 317 / 317 |
| September | 80 | 1.050282 | 5.03% | 317 / 317 |
| September | 110 | 1.021638 | 2.16% | 310 / 311 |

Five minimizing steps keep every selected hour. They are constant responses on the observed range, so their limits equal the ratio of mean ambient to heated ozone. The September 110-target optimum excludes seven heated and six ambient hours above 2.763839 kPa. Its limit is below the constant-response ratio of 1.026443. Thus the small limits mostly come from permitting a flat response, not an extreme selection of one hour. A requirement that the response must decline substantially can give a different result.

The common-scale upper bound at r=1 is zero in all 60 cases. Ten cases have zero excess above 40 ppb in both 30-target domes and have no finite reversal threshold. All 50 other cases have finite thresholds. For concentration, the high-target thresholds under the three alternate positive-light rules range from 1.01229 to 1.05908. Omitting the brightest hour alone gives high-target limits of 1.01329 to 1.05029. The low thresholds therefore do not depend on that one hour. The full all-hours and excess-40 results are in files/thresholds.csv. Excess-40 is a diagnostic and has no injury threshold interpretation here.

The smooth-response test gives a different scale. At the two high targets, S=2 kPa needs multipliers of 1.5187 to 1.8315. S=1 needs 2.2995 to 3.0977. S=0.5 needs 5.4014 to 8.1073. A 5 percent scale increase does not reverse any of these smooth examples. Small worst-case thresholds cannot be read as evidence that a small actual biological change reverses uptake. The response shape and its scale both matter.

All 50 nonzero thresholds matched linear programs within 1e-7. Direct step witnesses had negative and positive contrasts at r_star minus and plus 0.00001. An independent standard-library CSV parser and scalar saturation-pressure calculation checked all 60 rows. Its largest nonzero threshold discrepancy was 1.78e-15. Checks and full response frontiers are bundled. These are numerical checks, not new observations or uncertainty estimates.

## Meaning and open tests

The common-scale ranking is exact within its stated assumptions. It has a small scale margin for some permissive response shapes in these records. Our attempted robust extension to unequal scales therefore fails at modest multipliers in several cases. Yet the tested strongly declining smooth responses have much larger margins. We establish no measured multiplier and no probability that a reversal occurred.

Independent regions and years were not available in this small source. Temperature, light response beyond the gate, soil water, plant age, leaf boundary resistance and changing response shape were not fitted. The hourly data do not identify conductance or the scale ratio. Sensor errors were not bounded in this analysis. There is no estimate of a causal warming effect, flower timing shift, biodiversity loss or species range change. Repeated months do not repair chamber-treatment confounding.

The next useful test is to measure conductance in replicated heated and ambient chambers in separate years or regions. Those measurements should constrain both the response slope and its relative scale before a dose ranking is claimed. A uniform multiplier is only one departure from equal response. Hour-specific scale changes or different response shapes remain open. Code here can test the scale margin of other paired ozone-weather records with suitable local weather and calibration information.

## Reproduction, rights and worker record

Contains data supplied by UK Centre for Ecology & Hydrology.

The external source is under Open Government Licence v3. Raw data, supporting source documents and record-level derived data are not in this package. The package contains original code, narrative, aggregate optimization results and a figure. The SCI baseline applies to these bundled materials. It does not replace external source terms. Attribution and source terms are recorded in files/EXTERNAL_DATA_NOTICE.md.

We reused `/mnt/dell-data/shared_datasets/ukceh-wildflower-ozone-warming-2021-a33d5ee3/data.zip` in place. ZIP SHA-256: `d45d41b83dd1b8f147d90eba0c9cba3d12d05f9dd979f02378d631e8a8273d3a`. Hourly CSV SHA-256: `86c657edc758dd0012f7dff0cd673e9b49201ae41d8c8f90fdaac3e236e368ea`. All member hashes, source URL, release and software versions are in files/provenance.json. The design document was read to establish chamber assignments. Flower measurements were not fitted. No new download was needed.

With Python 3.12 and packages in files/requirements.txt, run from the extracted publication. Use fresh external paths:

```sh
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --raw /absolute/path/external/data.zip --fetch --out /absolute/path/rebuilt
python files/validate.py --raw /absolute/path/external/data.zip --results /absolute/path/rebuilt
```

Skip `--fetch` and pass the shared archive on this machine. Retrieval only occurs if the raw path is absent. The archive hash is enforced. If the provider changes its ZIP wrapper, inspect member hashes before adapting the code; do not silently accept a new version. Outputs and raw files must stay outside the signed publication. Compare the four aggregate CSV files numerically with the bundled copies. Paths in provenance and figure bytes can differ. Reproduction takes seconds and needs no private scratch or campaign cache.

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-3d9c3eb6fa5c. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. Analysis date 2026-11-12. The campaign-machine signature is not a personal authorship claim. No private key is included.
