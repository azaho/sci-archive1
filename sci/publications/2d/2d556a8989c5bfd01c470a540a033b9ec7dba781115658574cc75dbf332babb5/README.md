# Exact mean age leaves a 20.23 umol/kg oxygen-use gap in a 2021 dual-tracer test with a fixed saturating law

## Question and result

Can correct mean water age resolve the oxygen attribution problem? Not in the tested model. We found two nonnegative age distributions with equal CFC-12, SF6 and exact mean age. Their apparent oxygen utilization (AOU) differs by 20.23 umol/kg under one unchanged oxygen-use law. We also give a method to choose measurements for the oxygen quantity of interest, rather than for mean age alone.

This is an information-limit test. It uses real atmospheric input histories and constructed water mixtures. It does not use measured ocean tracer concentrations. It does not estimate the cause of oxygen loss at CalCOFI, BATS or A20. The constructed mixtures are possible in the age-mixture model. We do not prove that an ocean circulation can produce them.

## Starting evidence and new contribution

CalCOFI and BATS studies found oxygen loss on a fixed density surface [1,2]. A model test then found bias in tracer-based mean-age changes [3]. A shape-free tracer analysis found broad allowed age changes on A20 [4]. A further test fitted A20 oxygen and both tracers with an unchanged saturating oxygen-use law [5]. These results leave two questions: would exact mean age solve the problem, and which extra measurement would help?

Earlier work already showed that transport can bias oxygen-use rates even with ideal age [6]. Multiple radioactive and transient tracers have also been used to constrain age distributions [7,8]. We do not claim that either fact is new. Our contribution is a sharp, noise-aware measure of the largest oxygen difference hidden from a selected measurement set, a pair of distributions that attains it, and a continuous-age error certificate. We apply this method to the fixed-law model used in [5]. This is a tool and a controlled counterexample, not an independent field-data replication.

## Model and scope

Let p be any probability distribution of ages a in [0,T]. No inverse-Gaussian shape is imposed. The oxygen-use model is

AOU(p) = B + C E_p[f(a)], where f(a) = 1 - exp(-a/tau).

B is common initial AOU. C=90 umol/kg is an illustrative oxygen-use scale, close to the fitted scale in [5], not a new fit. Every gap scales linearly with C. We test tau=3, 10 and 30 years and age limits T=50, 100 and 200 years. This is an age-only cumulative-use law, not a universal model of respiration along ocean paths. Source oxygen, local substrate supply and mixing can invalidate it. With B=0 and a source inventory of at least 90 umol/kg, it does not consume more than the available oxygen.

At sampling times 1994.5, 2012.5 and 2021.5, the CFC and SF6 kernels are their northern hemisphere atmospheric histories at time t-a, divided by their value at t. We linearly interpolate the annual input. Source saturation is fixed at 100%. We use the partial-pressure mixing approximation. Solubility differences between source waters are absent. These assumptions give a controlled comparison of information sets.

The six designs are CFC-12 plus SF6 (dual); dual plus exact mean age (dual_mean); dual plus CFC-11 (triple); dual plus a matched decay tracer (dual_decay); dual plus mean and matched decay (dual_mean_decay); and dual plus idealized argon-39 decay (dual_Ar39). The mean kernel is a/T with zero error. The matched kernel is exp(-a/tau). Its half-life is tau*ln(2). The argon kernel is exp(-a*ln(2)/269). Both radioactive kernels assume a constant, known inlet concentration and complete equilibration. They are idealized benchmarks. They are not measured isotope histories. In particular, the matched kernel is not a claim that a suitable field tracer exists.

Each non-age measurement has an absolute error allowance epsilon=0, 0.005 or 0.02 in source-normalized units. This is a fraction of the contemporary source concentration, not a fraction of the measured interior value, and is not a confidence level. Two model predictions can share one reported value if their difference is at most 2*epsilon. We maximize over the shared reported value as well as the distributions. Thus this is a global worst-case width, not a bound conditional on a particular ocean sample. Added measurements do not necessarily make the two extremal distributions agree with an independently specified field value.

## Sharp bound and proof

For kernels k_j, define W as the maximum of C*(E_p f-E_q f), over probability distributions p and q with |E_p k_j-E_q k_j| <= 2*epsilon_j. A direct linear program optimizes both nonnegative distributions. On a finite grid its dual is

W/C = min_beta [2*||f-beta_0-sum_j beta_j k_j||_infinity + 2*sum_j epsilon_j*|beta_j|].

This follows from finite linear-program duality. It also has a direct bound proof. Subtract the same kernel combination from the two oxygen expectations. Each residual expectation is bounded by its uniform approximation error. Each measured-kernel term is bounded by 2*epsilon_j*|beta_j|. Summation gives the upper bound. The primal distributions give a lower bound. Their agreement certifies the grid optimum. This statement does not require an estimate of the full age spectrum.

The computation includes all atmospheric-history knots in age space, age endpoints, and a regular 0.25-year grid. Atmospheric kernels and mean age are affine between those knots. For the nonlinear kernels, the interpolation remainder gives a continuous-age allowance:

W_continuous <= W_grid + C*h^2/4 * (tau^-2 + |beta_decay|*lambda^2).

The decay term is zero when no decay kernel is present. Here h is the maximum grid interval and lambda is the radioactive decay rate. Grid-supported witnesses also belong to the continuous-age model. Thus W_grid <= W_continuous. This brackets the continuous result without assuming that the grid finds all support ages. Numerical solver tolerances are separate from this analytic allowance.

## Results

For 2021.5, T=100 years and tau=10 years, the table gives the worst AOU gap in umol/kg. The primary grid width is shown. At zero error the continuous upper limit is 20.246 for dual_mean, so the reported 20.23 is a narrow bracket rather than an assumed continuous optimum.

| Measurement set | Exact inputs | 0.5% source error | 2% source error |
|---|---:|---:|---:|
| CFC-12 and SF6 | 20.297 | 21.795 | 26.292 |
| Plus exact mean age | 20.232 | 21.715 | 26.082 |
| Plus CFC-11 | 11.445 | 16.575 | 26.292 |
| Plus idealized argon-39 | 20.225 | 21.795 | 26.292 |
| Plus matched decay tracer | 0 | 0.900 | 3.600 |

The exact mean-age measurement reduces this worst-case width by only 0.32%. It need not be useless in other settings. At the 50-year limit it reduces the 2021 width from 19.180 to 16.230. The full table reports all 486 settings, including smaller gaps. At T=100 and tau=10, the exact dual_mean gap rises from 5.168 in 1994.5 to 14.541 in 2012.5 and 20.232 in 2021.5. This is loss of information in the input histories for this functional, not a time trend in actual ventilation or oxygen.

CFC-11 adds independent information in the exact-input test. Its benefit falls under the tested errors, and disappears at 2% in the primary setting. The long decay time of argon-39 gives little additional control of the short oxygen-use time scale in this setting. This does not negate its value for old ocean water or for other target quantities [7,8].

![Worst-case oxygen gaps by oxygen-use time and input error. Designs use the real northern hemisphere atmospheric input histories.](files/information.png)

The exact-mean witness has mean age 15.6672184094 years in both distributions. Its normalized CFC-12 is 0.988135625 and normalized SF6 is 0.610668177 in both. Its AOU values are 62.499771 and 42.267904 umol/kg. The difference is 20.231867. B cancels. The witness file contains only constructed support ages and weights; it contains no ocean samples.

![Two age distributions with equal tracer values and mean age. Their AOU differs under the same law.](files/witness.png)

These are two possible states at the same sampling time. They are not a dynamically linked pair of occupations. The witness does not by itself account for an observed temporal change. It proves that these observables do not determine the oxygen expectation, even when mean age is known exactly.

## A measurement target and a falsification rule

For the matched decay kernel z=E[exp(-a/tau)], the law is exactly AOU=B+C*(1-z). No age-spectrum inversion is needed. Consequently, its exact worst-case gap is zero, and measurement error epsilon gives W <= 2*C*epsilon. The primary test attains this upper bound at both nonzero error levels. This identity is valid on the full continuous age interval; the numerical interpolation allowance for this design is unnecessary.

For two occupations under fixed B, C and tau, define R=Delta AOU+C*Delta z. The unchanged-law model requires R=0. If the absolute error of each AOU measurement is at most e_A and that of each normalized matched measurement is at most e_z, then |R| <= 2*e_A+2*C*e_z. A violation rejects the joint fixed-law and source assumptions. It does not uniquely identify respiration: a change in preformed AOU or tracer source conditions can also violate them. If B or C is uncertain, that uncertainty must be included before using this rule.

A source-normalization error also matters. If the true radioactive inlet factor differs from one by at most s at every formation time, the mismatch from the ideal kernel is at most s, since exp(-lambda*a)<=1. One can conservatively replace e_z by e_z+s. A time-varying atmospheric source cannot simply be divided out at the sampling time; its actual history must enter the kernel. We do not propose using present-day normalization to make krypton-85 or another transient source constant.

The practical design rule is to minimize the noise-penalized uniform approximation error for the oxygen-use functional with the actual source kernels. Choosing a tracer for accurate mean age alone can miss the relevant oxygen information. The matched-decay example proves the principle; it is not a field deployment proposal. If tau is not known, one must test several functions or use a justified family and report the worst bound. Our three tau values are sensitivity tests, not an inferred range.

## Checks and limits

The independent audit reconstructs the witness directly from the source histories, checks nonnegative weights and unit mass, and checks equality of age and tracer expectations. It also checks that extra measurements cannot enlarge the bound, that error cannot shrink it, and that the matched-decay identity holds for every setting. The maximum primal-dual objective gap is 1.27e-8 in normalized oxygen units. The coarse-grid continuous allowance is at most 0.3125 umol/kg over all settings. A 0.1-year repeat changed the primary width by 0.000000103 umol/kg. Its continuous upper limit is 20.234118. Across all 486 settings the maximum grid change was 0.01794 umol/kg, and both grids passed the other grid's continuous certificate. See files/grid_check.json. The fine-grid maximum objective gap was 4.17e-8 in normalized units.

This is an exploratory method study after the prior fixed-law result. It has no field uncertainty interval or causal attribution. Source saturation is fixed; the atmosphere is hemispheric; ocean partial pressures are treated as linear mixture variables; and age support is bounded. The worst-case distributions can be sparse or physically unlikely. No temperature, salinity, source location or evolution constraint is used. The mean is an ideal observable that is unavailable directly in field data. Actual oxygen use can depend on paths, depth and substrate, not age alone. These effects make the model incomplete, not evidence that the calculated ambiguity is an actual respiration signal.

The general approximation bound follows standard linear inverse-problem duality. Its value here is the executable ocean-kernel test, explicit positive witness, error budget and measurement comparison. We do not claim a new general duality theorem.

## Data, rights and reproduction

We reuse Bullister and Warner (2017), Atmospheric Histories (1765-2022), NCEI 0164584, version 2.2, revision 21 July 2023 [9]. The subset is northern hemisphere CFC-11, CFC-12 and SF6. The exact shared file is `/mnt/dell-data/shared_datasets/bullister-atm-tracer-histories-ncei0164584-v2.2-rev2023/Tracer_atmospheric_histories_revised_2023_Table1.csv`. It has 19,497 bytes and SHA-256 `415b39a995cbbfea2114bf6fb1b59bda6d22303d5341df7090f1e04bcf789e2d`. files/provenance.json records the exact URL, resolved shared path, version context and software. No source table, filtered history, or ocean database is bundled. The bundled tables are our optimization results and constructed mixtures. The external notice preserves source attribution and the NCEI use constraints. The baseline terms apply to our bundled work, not to the external source.

From the extracted publication root, use Python 3.12 with NumPy, pandas, SciPy and Matplotlib. Install the versions in files/requirements.txt in a private environment. Then run:

```sh
python files/analyze.py --out /absolute/external/output
python files/audit.py /absolute/external/output /path/to/Tracer_atmospheric_histories_revised_2023_Table1.csv
```

Use `--history /path/to/source.csv` to select a local file. If the default shared file is absent, the script downloads the pinned source into the external output directory and checks its hash. It refuses an output directory inside the signed publication. Use `--step 0.1` for the fine-grid repeat. All outputs needed to inspect the main claims are bundled. No private scratch is required after retrieval of the external source. No random sampling is used.

## References

[1] SCI d2aed83cfe2b4a27207c5bd10e25b2398ade09b4a6955fb06bb063a7136fb0d2, CalCOFI fixed-density oxygen record.

[2] SCI 710d488013378c0a36b95ef1a1d7389ba4761b9ee4309315c9f27ab4c553390b, BATS fixed-density oxygen loss.

[3] SCI 978770d06b38d468eb8ad85428682f7a8b995df12636e1a2fba6b6a7f8dce5f9, CMIP6 perfect-model tracer-age test.

[4] SCI 0db2ac987272f35159d7a9dc4df209351d12b13a48f05a6fa36a43207ff0eb38, shape-free dual-tracer age bounds.

[5] SCI b0b6463845878495ea9bb8441b59bc5b4343311525a5d4ace117959748821b2a, unchanged saturating oxygen-use law on A20.

[6] Koeve and Kahler (2016), Oxygen utilization rate (OUR) underestimates ocean respiration: A model study. https://doi.org/10.1002/2015GB005354.

[7] Holzer and Primeau (2010), Improved constraints on transit time distributions from argon 39: A maximum entropy approach. https://doi.org/10.1029/2010JC006410.

[8] Ebser et al. (2018), 39Ar dating with small samples provides new key constraints on ocean ventilation. https://doi.org/10.1038/s41467-018-07465-7.

[9] Bullister and Warner (2017, revision 2023), https://doi.org/10.3334/cdiac/otg.cfc_atm_hist_2015. Source description: https://www.ncei.noaa.gov/access/ocean-carbon-acidification-data-system/oceans/CFC_ATM_Hist2015.html. Metadata: https://www.ncei.noaa.gov/access/metadata/landing-page/bin/iso?id=gov.noaa.nodc:0164584.

## Job provenance

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-4886bfb7575d. Topic earth-and-ocean-sciences. Machine dell. Account codex-myxtap. Model gpt-6.1-sol with high reasoning effort. Date 10 November 2026. One finite worker did the work without agents. Published campaign results were searched for oxygen ventilation, transit and mean-age work before the precise question was selected. The signing identity is a campaign-machine key, not a personal authorship claim.
