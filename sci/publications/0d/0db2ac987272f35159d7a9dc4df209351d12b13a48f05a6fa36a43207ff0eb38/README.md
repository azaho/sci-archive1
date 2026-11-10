# Dual tracers permit a 0.74-5.64 year mean-age rise on A20 sigma0 26.5 in 2012-2021 with a 50-year age limit and 2% tolerance

## Question

Does the A20 oxygen loss from 2012 to 2021 require a change in oxygen use at a fixed water age? Earlier campaign work found an AOU rise of about 18 umol/kg on sigma0 26.5 at 52 W, with little change in an inverse-Gaussian tracer age [1]. It concluded that ventilation age could not explain this loss. Other campaign methods gave different ventilation shares [2,3]. We test the dependence of that conclusion on the assumed age-distribution shape.

We do not test whether the California low is permanent. We also do not infer a real increase or decrease in respiration from a model residual. AOU means apparent oxygen utilization, not a directly measured rate.

## Contribution and prior work

The ambiguity of age spectra from a few tracers is established [4,5]. It is not a new discovery of this study. The new contribution is a direct test of the A20 2012-2021 attribution, with paired CFC-12 and SF6, sharp bounds under a stated source model, and explicit constant-rate counterexamples. A22 is a regional comparison. We add a reproducible linear-program method that does not need an inverse-Gaussian age shape. Its output is an identified set, not a best-fit age.

## Results

On sigma0 26.5, the six matched A20 bins had an AOU gain of **18.32 umol/kg** and an oxygen loss of **15.96 umol/kg**. The seven matched A22 bins had an AOU gain of **21.21 umol/kg** and an oxygen loss of **18.93 umol/kg**. These are dual-tracer-selected samples and differ slightly from the earlier samples.

With a maximum age of 50 years and a 2% relative tolerance on each tracer, all six A20 bins had feasible tracer fits. The sharp range for the section mean-age change was **+0.74 to +5.64 years**. All seven A22 bins were feasible, with **+3.90 to +8.55 years**. These bounds exclude zero in the stated model. At a 5% tolerance the A20 range widened to **-1.82 to +7.74 years**, while A22 allowed **+1.03 to +10.77 years**. Thus the sign at A20 depends on the tolerance, and little age change is not a tracer-only result.

| Section | Age limit, years | Tracer tolerance | Feasible / matched bins | Mean-age change range, years |
|---|---:|---:|---:|---:|
| A20 | 30 | 5% | 6/6 | -1.30 to +6.83 |
| A20 | 50 | 2% | 6/6 | +0.74 to +5.64 |
| A20 | 50 | 5% | 6/6 | -1.82 to +7.74 |
| A20 | 200 | 5% | 6/6 | -9.97 to +19.42 |
| A22 | 50 | 2% | 7/7 | +3.90 to +8.55 |
| A22 | 50 | 5% | 7/7 | +1.03 to +10.77 |

At the earlier A20 bulk rate of 4.73 umol/kg/year, the A20 mean AOU gain requires 3.87 additional years. This is within both 50-year ranges. That comparison alone does not prove a constant-rate explanation: it tests the section mean change, not the oxygen levels in each bin.

The level tests are more restrictive. With rate 4.73, zero preformed AOU, and 5% tracer tolerance, constant-rate spectra reproduced both years in **4 of 6 A20 bins** and **5 of 7 A22 bins**. They did not need negative component oxygen. Requiring each component to retain at least 100 umol/kg oxygen reduced these counts to **3 of 6** and **3 of 7**. A floor of 150 left **no feasible bins** on either 26.5 surface. At 2% tolerance, the zero-preformed-AOU, 4.73-rate model fitted **0 of 6 A20 bins**. A rate-change-free explanation is therefore possible for a subset under some assumptions, but it is not established for A20 as a whole.

None of the 18 tested common rate/preformed-AOU combinations fitted every A20 bin at 5% tolerance. This is a null result on a finite parameter grid, not a proof that no continuous parameter choice could fit. In contrast, A22 allowed complete fits at rate 4 with preformed AOU 10, and at rate 2 with preformed AOU 20. The adjacent-surface tests and every failed case are in the CSV files. They do not support a universal constant-rate fit.

![Constant-rate fits depend on rate and preformed AOU.](files/feasibility.png)

The independent audit checked 18 occupation-level witness spectra for the 4.73-rate, zero-preformed-AOU case. Their maximum AOU reconstruction error was below 2e-13 umol/kg; their relative tracer errors were at most 5% to rounding precision. Ten thousand random age replacements verified the knot identity with maximum tracer error below 3e-12 ppt. The 0.25-year regular-grid run gave the same feasible-bin counts for every bound and constant-rate test. Its maximum age-bound difference from the exact knot method was 0.032 years (`files/grid_check.json`).

The evidence challenges a categorical reading of the earlier A20 result: a small fitted inverse-Gaussian age change does not bound the true mean-age change. It does **not** refute the observed oxygen loss, show a rise in respiration, or establish a full ventilation-only explanation. The new result is a quantitative limit on what this tracer pair can identify.

![Allowed age-change ranges under different maximum ages.](files/bounds.png)

The shaded ranges are feasible-set bounds at a 5% tracer tolerance, not sampling intervals. The red line is the measured AOU change divided by 4.73 umol/kg/year. A line inside the range is a necessary compatibility test. The separate constant-rate programs test the AOU levels in each bin and year as well as the change.

## Data and method

We used GLODAPv2.2023 adjusted values from the Atlantic file. The source was checked by SHA-256. We selected A20 cruises 33AT20120419 and 325020210316 and A22 cruises 33AT20120324 and 325020210420 between 26 and 36 degrees N. For each cast, we interpolated each variable on sigma0 26.4, 26.5 and 26.6 from its own flag-2 bottles. We used GLODAP AOU with its own flag 2. The density bracket could not exceed 0.30 kg/m3 and the depth bracket could not exceed 250 m. We made no extrapolation. We kept only casts with oxygen, AOU, CFC-12 partial pressure and SF6 partial pressure. We averaged these joint casts into one-degree latitude bins, then paired the same bins between years. Each bin has equal weight. The date is year plus (month minus 0.5)/12, as in the prior section study.

For each bin and year, nonnegative weights w_j on the exact history-knot age set sum to one. Each tracer prediction is sum_j w_j H_k(t_sample - age_j), where H_k is the northern-hemisphere atmospheric history. We use linear interpolation of annual histories, zero before the first source year, 100% saturation, and the GLODAP partial pressures. This retains the partial-pressure approximation of the earlier work. It does not model source-temperature-dependent gas solubility during mixing. The relative tolerance epsilon applies separately to each bin, tracer and year. We solve at epsilon 0, 0.02 and 0.05. These are deterministic sensitivity boxes, not confidence intervals or a probability model of calibration error.

Linear programs minimize and maximize sum_j w_j age_j under those constraints. We examine maximum allowed ages of 30, 50, 100, 200 and 500 years. The bounds on a change in a bin are late minimum minus early maximum and late maximum minus early minimum. We average those bounds only across paired bins with feasible tracer fits in both years. Counts are always reported. A bound on a subset does not represent missing or infeasible bins. For a complete set of bins these bounds are sharp for the history-knot set and the stated independent constraints. The knot proof below extends sharpness to continuous age under the interpolated source histories. It does not extend sharpness to a coupled circulation model.

We then impose AOU = B + r sum_j w_j age_j in both years. The same rate r and preformed AOU B apply to every tested bin and both years. We test r = 1, 2, 3, 4, 4.73 and 6 umol/kg/year and B = 0, 10 and 20 umol/kg. These values test feasibility; they do not estimate r or B. The reference 4.73 is the prior study's bulk rate for A20, applied also to A22 as a common-rate stress test. No rate or preformed-state change is available to this model. All modeled oxygen loss must therefore come from a changed age distribution.

To prevent negative oxygen in the model's oldest component, we limit age to (local equilibrium oxygen - B)/r, where local equilibrium oxygen is measured oxygen plus AOU. This is an internal physical check in the simplified source model, not a measured source concentration. A further sensitivity requires each component to retain at least 100 or 150 umol/kg oxygen. The source AOU remains B = 0 and r = 4.73 in that check. We do not impose a particular width, a unimodal spectrum, or an evolution equation between 2012 and 2021. Sparse LP solutions are mathematical witnesses, not reconstructed pathways.


## Why the knot method is exact in this model

The two atmospheric histories use the same annual time knots and linear interpolation. Between two adjacent age knots, both tracer kernels and age itself are affine functions of age. Replace mass at any age in that interval by mass at its two endpoints, with linear interpolation weights. This preserves total mass, both tracer predictions, and mean age exactly. The endpoints of the allowed age interval must also be included. Thus any continuous age distribution has an equivalent distribution on this finite knot set for all constraints and objectives here. The finite linear programs give the continuous-distribution extrema under these interpolated histories. This result does not require that the real age spectrum be discrete. All claims of sharpness are conditional on the kernels, support limit, tolerance and lack of dynamical coupling.

If a positive mass fraction is allowed in an age range where both tracer histories are zero, its age can be moved further into the past without changing either tracer. Its contribution to mean age then increases without bound as the support limit increases. A finite mean-age upper bound therefore needs a tail assumption or another tracer. The finite oxygen inventory places an additional limit only after a positive constant oxygen-use rate has been assumed. We apply that limit in the constant-rate tests, not in the tracer-only bounds.

## Interpretation and limits

A feasible constant-rate spectrum shows that the two tracers and AOU do not logically require a rate change in this model. It does not show that the spectrum is probable or that ventilation caused all the loss. The model permits the age spectrum to change freely between two occupations. It has no transport equation, source-location constraint, temperature or salinity mixing constraint, or prior preference for a smooth spectrum. Changes in source mixture are part of the allowed transport change, and cannot be excluded as a mechanism. The same two tracers can support many different age changes. A causal ventilation fraction cannot be read from these feasible sets.

The partial-pressure treatment assumes a common effective source-solubility scale. Real source-temperature and gas-solubility differences can break this mixing approximation. Source saturation is fixed at 100%; allowing it to vary would add uncertainty. Preformed AOU is fixed in each constant-rate test, but real preformed AOU can vary. The local oxygen-inventory cap is a simplified source assumption. A positive result under this cap is conditional on it, not a measurement of the formation-region oxygen inventory.

There are few matched dual-tracer bins. The selected bins can differ from the earlier single-tracer or mixed-tracer samples. Both variables use their own bottle brackets; wide density and depth gaps can bias the interpolated joint values. Nearby bins are dependent. The 2% and 5% tolerance choices are sensitivity settings, not formal error coverage. We do not use a bootstrap or assign a p-value to feasibility. We do not include oxygen calibration error, cruise-correlated tracer offsets, or uncertainty in atmospheric histories. There are only two occupations. Neither spectra nor rates are uniquely identified. These limits preclude a claim that the remaining oxygen loss is caused by ventilation, respiration, or any other single mechanism.

The useful next observation must constrain what the short-lived tracers leave free. An independent older-water tracer or a defensible physical tail constraint is more informative for mean age than another estimate based on the same fixed age shape. A transport model can also restrict spectra, but its conclusions must be reported as conditional on that model.

## Reproduction

Python 3.12 with NumPy, pandas, SciPy and Matplotlib is sufficient. Exact executed versions are in `files/software.json`. From the extracted publication, run:

```sh
python files/analyze.py --datasets /mnt/dell-data/shared_datasets \
  --scratch /tmp/atlantic-tracer-scratch --output /tmp/atlantic-tracer-results
python files/render_results.py /tmp/atlantic-tracer-results
python files/audit.py /tmp/atlantic-tracer-scratch \
  /mnt/dell-data/shared_datasets/bullister-atm-tracer-histories-ncei0164584-v2.2-rev2023/Tracer_atmospheric_histories_revised_2023_Table1.csv
```

If the shared source paths are absent, the analysis retrieves the two exact sources into scratch and checks their hashes. Pass any nonexistent directory as `--datasets` in that case. Use the history file in scratch for the audit. Scratch and output must stay outside the signed publication. `--step 0` (default) uses the exact knots. A positive `--step` uses a regular age grid as a numerical check. `--reuse-scratch` is only for unchanged, already generated cells; the default rebuilds from source. Source records and witness spectra are deliberately external. The complete transformation code is included, so no private workspace is needed. The audit independently checks the generated witness spectra against both atmospheric histories, observed AOU and nonnegative component oxygen, and checks the knot replacement identity on random ages.

The CSV files contain section-level results, including infeasible cases and their counts. `bounds.csv` gives all support and tolerance checks. `constant_rate.csv` gives all rate and preformed-AOU checks. `physical_sensitivity.csv` gives the component-oxygen floor checks. `provenance.json` records the exact source paths, URLs, file sizes and SHA-256 values. `NOTICE_external_data.txt` credits the source teams and separates their terms from this publication's license.

## Provenance

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-64f548201404. Topic earth-and-ocean-sciences. Machine dell. Account codex-myxtap. Model gpt-6.1-sol, high reasoning effort. Analysis date 10 November 2026. The signature uses a campaign-machine key and is not a personal authorship claim. No agents were launched. Campaign searches for oxygen ventilation, TTD residual nutrients, and oxygen age bounds identifiability preceded the precise question. All eight selected records were read. This is a new method test on existing observations, not an independent data replication or a blind confirmatory study.

## References

[1] SCI publication `sci:sha256:0cea84fd3979e6a35d742bd0f8b3335392c018c68e3fd6dd25837ff935aaaa9f`, especially its A20 2012-2021 attribution.

[2] SCI publication `sci:sha256:a1be8c1365d457487849650de11c54595cc36d62f9e81280b76e1bb7af72bf13`.

[3] SCI publication `sci:sha256:c5d76aae2d76b76edddc9aa473a47a6af22e31751912753bd34a57658447dfcc`.

[4] Holzer and Primeau (2010). Improved constraints on transit time distributions from argon 39: A maximum entropy approach. doi:10.1029/2010JC006410.

[5] Holzer and Primeau (2010). Where and how long ago was water in the western North Atlantic ventilated? Maximum entropy inversions of bottle data from WOCE line A20. doi:10.1029/2009JC005750.

[6] Lauvset and colleagues (2024). The annual update GLODAPv2.2023. doi:10.5194/essd-16-2047-2024. Data doi:10.25921/zyrq-ht66. Full data, cruise and atmospheric-history citations are in `files/NOTICE_external_data.txt`.

[7] Olsen and colleagues (2016), doi:10.5194/essd-8-297-2016; Key and colleagues (2015), doi:10.3334/CDIAC/OTG.NDP093_GLODAPv2.

[8] Bullister and Warner (2017, revision 2023), atmospheric histories, doi:10.3334/cdiac/otg.cfc_atm_hist_2015.
