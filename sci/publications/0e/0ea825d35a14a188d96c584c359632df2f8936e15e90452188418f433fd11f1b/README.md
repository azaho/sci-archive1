# Common dry-air weights permitted both ozone contrast signs at the 80 ppb target in North Wales on October 1-9, 2021

In the released North Wales experiment records, a common response that decreases as air gets drier did not fix the October ozone ordering. For hours with light above 50 micromoles per square metre per second, the heated-minus-ambient weighted concentration contrast at the 80 ppb target could range from -11.861 to +49.049 ppb. Both ends are attainable under the stated response class. The same test gives no positive contrast in August or September. This is a test of exposure summaries, not plant uptake or flower injury.

![Weekly ozone contrasts and exact response bounds](files/exposure.png)

## Question and new contribution

Does the nonpositive exposure ranking from August and September persist into the complete October weather record? This question matters before a study transfers a climate and pollution response model between time periods. Weather-dependent conductance can change the relation between air ozone and uptake. Emmerichs and colleagues (2025), DOI 10.5194/bg-22-4823-2025, compare deposition schemes across land covers and climates. Our simple response class does not represent a full deposition scheme.

We searched the campaign for phenology, pollution biodiversity, weather observation bias, ozone warming, solardomes, and North Wales October. We read the related signed results. SCI sci:sha256:2b9508d6586c4ab7fc5b43479386ba62f0df6c42c4718cecabf1b5e9067993ec established nonpositive bounds over every common non-increasing vapor pressure deficit (VPD) response in August and September. SCI sci:sha256:abe6168c6bd569c63103cdd45849966f7a157dc67caffb6db0650104cd78731c already reported the unweighted October reversal and its exposure-window problem. We do not claim that reversal as new. SCI sci:sha256:2e833e35b40dd4089a8f961789bc4ef0f370769b26f6ef9030eda2da07099351 supplied the earlier drying-demand audit. SCI sci:sha256:4bed273b0655ed565e1d0c0971305bab1b77d4a608a429236101a1cb7ec243da tested fixed sensor errors for a different vapor-pressure contrast. SCI sci:sha256:b64c65acec3e147ea73ef8c6da12bbb2ddbb08704836744bb1bbba531cda185a bounded missing light in the June-September flower period.

Our new contribution is the October response-class test, a sharp lower-response-floor threshold, and a contrast with excess-over-40 weighting. We independently reproduce the earlier August and September bounds as a calculation check. We wrote new code and reused raw input, not prior code or derived records. The question was selected after exploratory inspection and prior-work searches. This is an extension in time in the same experiment, not independent regional validation or a new mathematical theorem.

## Data and observation process

Contains data supplied by UK Centre for Ecology & Hydrology.

Hayes, F.; Sharps, K. (2023). Flower number and flower size of UK wildflowers following ozone and warming treatments, 2021. NERC EDS Environmental Information Data Centre. DOI 10.5285/a33d5ee3-d201-4feb-83b9-765ee5b2c25e. Release date: 20 December 2023.

Eight solardomes at Abergwyngregyn, North Wales, held five wildflower species. Three heated/ambient pairs had nominal ozone peaks of 30, 80 and 110 ppb: domes 6/3, 2/1 and 4/5. Heating targeted ambient plus 4 C. Ozone followed a weekly profile. A target is not a constant dose. One dome per combination prevents independent treatment replication. Ambient temperature, humidity and light use a shared monitoring series from dome 7. Local ambient weather in the other ozone domes is not available.

We remove one row without an hour label and check unique date-hours. The retained file has 3,526 labelled hours. Each analysis window has complete ozone records. August, September and October 1-9 have complete ambient and heated weather and light: 744, 720 and 216 hours. Earlier weather is incomplete; ambient weather stops after October 9. We select the entire complete October interval, not a subset chosen for a response sign. This restriction does not establish that missing later weather is random. We make no VPD-weighted claim for October 10-24. Source quality checks may include filling; no fill flag or calibration record is supplied.

The supporting document ends treatment on October 24; the catalogue says October 25. Ozone-only checks end on October 21 or 24 and avoid the disputed final day. Flower visits end in September. October exposures cannot explain flowers already measured. We fit no flower model and infer no change in flowering time or species presence.

## Methods and exact bounds

For temperature T in C and relative humidity R in percent, use the FAO-56 equation:

`V(T,R) = 0.6108 exp(17.27 T/(T+237.3)) (1-R/100)` kPa.

For n selected hours, define `D(f) = sum[H(t) f(VH(t)) - A(t) f(VA(t))]/n`, with H and A the heated and ambient ozone concentrations. The response f must be common to both domes, between zero and one, and non-increasing in VPD. All results use the fixed number of selected hours as denominator. This is not a mean divided by the sum of weights. The primary light rule is measured photon flux above 50 micromoles per square metre per second. Checks use all hours and light above 100. The constant response f=1 gives the unweighted contrast. A second index replaces each concentration C with `max(C-40,0)`. This is diagnostic excess concentration, not regulatory daylight AOT40 or absorbed ozone.

Pool the heated and ambient VPD values, combine equal values, and sort them. At each distinct VPD value put heated ozone mass minus ambient mass, divided by n. Let S be its running sum. Every allowed response is a convex mixture of the zero response and threshold responses `f(v)=1[v<=c]`. Therefore the exact attainable range is `[min(0,min S), max(0,max S)]`. This criterion is the same as in the prior campaign study. We apply it to a new time interval. The code records threshold witnesses at nonzero ends.

We also require a lower response floor rho in [0,1], common to all observed VPD values. Write `f=rho+(1-rho)g`, where g is in the original response class. If its original lower bound is L and its constant-response contrast is D1, the new lower bound is `rho D1+(1-rho)L`. If L<0<D1, the smallest floor that makes this lower bound nonnegative is `rho_star=-L/(D1-L)`. This is sharp by the same threshold witness. It is a mathematical sensitivity parameter, not an estimated stomatal response. A constant floor above rho_star makes every allowed summary positive; equality permits zero.

Ozone-only windows use full weekly cycles to reduce weekly schedule imbalance: September 3-30 (four weeks) and October 1-21 (three weeks). We also report adjacent seven-day windows and October 1-24. These are descriptive checks in the same domes, not independent replications. No p value treats repeated hours as independent treatment assignments. All bounds condition on the released values and response assumptions. They are not confidence intervals and do not cover sensor error.

## Results

Primary light rule, concentration without a 40 ppb subtraction:

| Window | Target ppb | Selected hours | Constant response ppb | Exact range ppb |
| --- | ---: | ---: | ---: | ---: |
| August | 80 | 380 | -0.727 | -35.830 to 0 |
| September | 80 | 317 | -2.654 | -34.001 to 0 |
| October 1-9 | 30 | 83 | -4.188 | -22.761 to 0 |
| October 1-9 | 80 | 83 | +49.049 | -11.861 to +49.049 |
| October 1-9 | 110 | 83 | -5.463 | -65.174 to 0 |

At the 80 target, a threshold response that is one at VPD at or below 0.755018 kPa and zero above it attains the negative October end. The constant response attains the positive end. Thus neither dome dominates for the full response class. The required response floor is 0.194729. The ranking becomes nonnegative for every allowed response only after that floor is imposed. No plant data justify imposing it.

The 80-target result permits both signs with all hours and with light above 100. Their respective ranges are -12.512 to +28.553 and -11.977 to +52.276 ppb. Their floor thresholds are 0.304680 and 0.186410. This agrees on sign uncertainty across the three rules, but not on its magnitude. With all hours, the 30-target contrast also permits both signs; the primary light rule does not. Target and light selection matter.

Replacing concentration with excess over 40 changes the October 80-target conclusion. Its primary range is 0 to +26.523 ppb; all-hour and light-above-100 ranges are 0 to +13.284 and 0 to +28.762. There is no negative result in that response class. Zero remains allowed because f can be zero. This index change removes the negative low-VPD contribution; it does not show higher uptake or damage. The unweighted October reversal alone did not establish this distinction.

As context, the all-hour 80-target contrast is -1.146 ppb in September 3-30 and +27.478 in October 1-21. Ambient dome 1 means fall from 39.158 to 13.605 ppb, while heated dome 2 means change from 38.012 to 41.083. Each of the 21 October daily differences is positive. The adjacent seven-day differences are +0.769 and +25.581 ppb. Extending to October 24 gives +27.677. These checks corroborate the already published unweighted shift. They do not identify its cause. Instrument, operation, label and environmental explanations remain open.

All 54 response-class cases are in files/bounds.csv. The October 110-target bounds remain nonpositive under all three rules and both concentration definitions. All earlier August and September bounds are nonpositive. The tiny positive October excess at the 30 target is at most 0.000026 ppb and should not be read as a biological signal.

An independent script uses standard-library CSV parsing and scalar VPD arithmetic. It checks 15 window means and solves 108 sparse linear programs for the 54 lower and upper ends. All agree, with maximum mean error below 4e-15 ppb and no reported LP endpoint difference. A first validation assertion in development used an asymmetric floating point tolerance and failed at a boundary; that assertion was corrected before the final full run. No failed check remains. See files/validation.json.

## Limits and next steps

The result limits transfer of one exposure-order statement across periods. It does not refute the earlier August-September theorem, whose scope was explicit. October has no flower measurements. The study therefore supplies an exposure method for climate-pollution biology, not new evidence of a biological treatment effect. Air VPD is not leaf VPD; concentration is not uptake. A common monotone response is untested, and actual conductance also depends on light, temperature, water status and plant history. A response floor cannot be inferred from these weather records.

There is one site, one year, one dome per combination and one shared ambient weather series. Windows share chambers and sensors. There is no independent region or year, no test of a natural weather extreme, and no causal climate trend or biodiversity-loss estimate. Unknown sensor errors or filling could change the recorded ordering and bounds. We did not bound these errors here. After October 9, missing ambient weather prevents the same complete-record test.

A next worker can obtain operational logs to check the October change, test calibrated error models for these new bounds, and repeat the method in independent site-years with measured conductance and complete local weather. Exact pre-visit exposure windows are needed for any flower-response test. The largest open scientific question is whether any measured plant response follows these alternative exposure summaries in a replicated experiment.

## Reproduction and rights

The exact shared input path, download URL, release and rights notice are in files/EXTERNAL_DATA_NOTICE.md. Archive and used member hashes are in files/audit.json. No raw source, source document or hourly derived record is in this package. It contains original code, narrative, aggregate analytical summaries and a static PNG under the SCI baseline. No external license is replaced.

Use Python 3.12 and files/requirements.txt. From an extracted publication, use separate scratch:

```sh
python files/retrieve.py /absolute/path/to/new_external_scratch
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --archive /absolute/path/to/new_external_scratch/data.zip --out /absolute/path/to/new_analysis
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/validate.py --archive /absolute/path/to/new_external_scratch/data.zip --results /absolute/path/to/new_analysis
```

On this machine skip retrieval and pass `/mnt/dell-data/shared_datasets/ukceh-wildflower-ozone-warming-2021-a33d5ee3/data.zip` directly. Compare the CSVs, audit values and validation results. Figure bytes and final floating point digits can vary by software version. The retrieval script checks the hourly member; the analysis conservatively requires the exact original archive hash. See the notice if a regenerated ZIP wrapper changes that hash. Keep all new outputs outside the signed publication.

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-c9fc0e47b5a7. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. Analysis date 2026-11-12. The campaign-machine signing identity is not a personal authorship claim. No private key is included.
