# A full-rank tracer mass balance identifies storage, recharge and evaporation in one changing mixed store

A known tracer mass source can remove a storage-scale ambiguity that natural tracer concentrations leave unresolved. We prove a full-rank condition for one fully mixed store with freely changing flux histories. Under this condition, three tracer records identify storage, recharge and evaporation. Measured streamflow then gives cumulative non-stream liquid loss from water balance. The condition concerns the mass that reaches the mixed store, not only the mass applied at a field site. The result is a method and a synthetic test. It does not identify the cause of the Australian runoff loss.

## Question and prior work

The selected SCI work reports a large runoff loss after 1997. It also reports faster flow decline. Neither observation alone identifies the missing water path. SCI c8882d21 found that the pooled decline signal survived matching on dry-spell age, but it limited a claim of sustained faster slow-store drainage. SCI e813e246 proved that changing storage scale can preserve flow and natural tracer records through a continuous transition. SCI d7dec7a0 showed that known fractionation and total evapotranspiration can still leave scale uncertain when plant uptake can shift between stores. We read these published results before choosing this question.

Can a measured tracer mass source remove that freedom, and for how long? Tracer injection, dilution gauging and tracer-based inverse models are established methods. Kelleher et al. (2013), doi:10.1002/wrcr.20413, found parameter-identification problems in stream pulse tests. Wlostowski et al. (2013), doi:10.1002/wrcr.20103, compared constant-rate and slug injection designs. Bonanno et al. (2022), doi:10.5194/hess-26-6003-2022, developed a stream transport identification analysis. Those models concern stream transport; our theorem concerns a changing single water store. Fowler et al. (2022), doi:10.5194/hess-26-6073-2022, review proposed Australian causes.

Our contribution is the combined three-column identification test, its limit outside injection support, and a reproducible noise test of cumulative loss. We do not claim to invent tracer mass balance or tracer injection. The study is exploratory. No field data were fitted and no analysis plan was registered. The preceding ambiguity results suggested the question but do not serve as independent empirical evidence for this method.

## Model and proof

Let S be positive storage, I recharge, Q measured streamflow, E evaporation and L other non-stream liquid export. All exports except evaporation carry the store concentration C. A tracer has known recharge concentration u, known decay mu and known evaporation concentration alpha*C. A separate source adds mass J to the mixed store with negligible added water. Put beta=1-alpha. Then

    S' = I-Q-L-E
    C' + mu*C = (u-C)*(I/S) + beta*C*(E/S) + J*(1/S).

For each time, stack the tracer equations into y=A*x. The three columns of A are u-C, beta*C and J. If A has rank three, x=(I/S,E/S,1/S) is unique. Hence S, I and E are unique. This holds even when their process laws change with time. It requires exact concentration records and derivatives. A nonphysical inverse solution rejects the assumed model or inputs; it is not a physical flux estimate.

A useful balance follows without differentiating reconstructed storage:

    integral L = integral [(I/S-E/S)/(1/S)-Q] - (S_end-S_start).

This reduces one noise source, but endpoint storage and tracer derivative errors remain. L includes any nonfractionating plant uptake from this store. The method cannot separate that uptake from groundwater leakage or locate the exported water. If all such plant uptake is absent or independently measured, this residual has a narrower liquid-export interpretation.

On a rank-deficient interval, smooth null directions can give distinct positive flux histories with the same observations. A known injection source blocks the scale transformation only where that source is nonzero. After injection ends, a smooth scale change can again preserve every concentration and Q. A known instantaneous pulse can anchor one instant under complete mixing; it does not fix a freely changing future store. Unknown recovery of the administered dose also restores ambiguity. The full proofs, qualifications and a perturbation bound are in files/THEORY.md.

## Synthetic experiment

![Synthetic intervention tests](files/results/design.png)

All inputs are synthetic. Time is 0-60 days, with samples each 0.25 day. Storage is 30+2 sin(t/15) mm. Recharge is 0.95+0.12 sin(t/9), evaporation is 0.12+0.02 cos(t/11), and streamflow is 0.45+0.04 sin(t/13), all in mm/day. L closes water balance and stays positive. These choices give time-varying rates without imposing a fixed stream-to-store law.

Three virtual tracer concentrations start at (0.3,1,0), with constant recharge concentrations (2,1,0), zero decay and evaporation contrasts (0,b,1). The third tracer receives a constant mass source j. These are mathematical tracers in arbitrary consistent concentration units. They are not proposed chemicals or a calibrated isotope experiment. The determinant is (2-C1)*b*C2*j. It is nonzero in all nine combinations of b and j tested. Setting j=0 gives rank two. Setting b=0 also prevents three independent columns in this design.

We integrate tracer masses, then invert their exact concentration derivatives. All nine exact cases recover the rates with maximum absolute error below 3.5e-16 in the stated units. This checks algebra and implementation, not field accuracy. An independent triangular solution agrees with the matrix solution within 1.4e-17. Integrated loss over all 60 days differs from the known value by 0.000036 mm due to quadrature.

To test finite records, we add independent Gaussian concentration errors with SD 0, 0.0001 or 0.001. We use a 41-point cubic Savitzky-Golay smoother and its derivative, then invert days 5-55. The 10-day smoothing window and fixed edge exclusion apply to every case. Each nonzero noise case has 200 seeded simulations, for 3,600 noisy runs in total. The same method is not tuned to each outcome. No negative estimate is clipped or removed. A run is flagged if any scored S is nonpositive or any I or E is negative. This flag does not test the positivity of instantaneous reconstructed L.

At noise SD 0.001, the results are:

| b | j | Median storage error | Median evaporation error | Cumulative L error, 2.5% to 97.5% | Runs with flagged estimates |
| ---: | ---: | ---: | ---: | ---: | ---: |
| 0.2 | 0.2 | 1.65% | 13.2% | -8.2% to +9.0% | 0/200 |
| 0.2 | 0.02 | 14.1% | 18.6% | -88.8% to +120.0% | 0/200 |
| 0.2 | 0.002 | 74.3% | 75.2% | -3411% to +1909% | 200/200 |
| 0.02 | 0.2 | 7.68% | 129.6% | -85.5% to +41.1% | 200/200 |
| 0.002 | 0.2 | 57.5% | 945.2% | -1701% to +6260% | 200/200 |

Storage and evaporation errors are the median across runs of the within-run median absolute relative error. Loss errors are signed errors in the integral over days 5-55, relative to its true value. The ranges are simulation quantiles, not confidence intervals for a field basin. All runs, including flagged ones, enter these summaries. Near-zero or negative inverse storage rates can give extreme signed estimates. These are method failures, not unusual physical losses. A positive estimate alone is also insufficient: the second row has no flagged runs but very large loss error.

The sensitivity result matters. Algebraic uniqueness does not ensure a useful water-loss estimate. Smaller mass input and smaller fractionation contrast can cause severe instability even with known input concentrations, known fractionation, no mass-delivery error and the correct store model. The error threshold is specific to these arbitrary concentration units and this virtual design. It is not a permissible field dose or an Australian measurement requirement.

## Injection support test

A separate audit stops injection at day 20. It compares two independently integrated water and mass systems. They start identically. The alternative storage scale is one before day 25 and after day 55; between these dates it has a smooth positive bump that peaks at 1.1. Recharge and evaporation scale with it, and liquid export changes by the exact balance formula. The alternative liquid export remains positive, with minimum about 0.01193 mm/day. Streamflow is held equal through a freely changing discharge law.

The stores differ by 10%, while concentration records agree within 6.4e-14. This is a constructive failure of permanent calibration after injection ends. It does not show that a pulse cannot identify parameters of a fixed model. It shows why a pulse cannot identify arbitrary future changes without more assumptions.

## Use and limits

The rank test supplies a clear design target: independent recharge and evaporation contrasts, plus a calibrated mass input into the store being observed. A field study would first need evidence that its tracers sample that store, that fractionation and other tracer losses are known, and that the applied mass actually reaches it. Two water isotopes can have nearly dependent contrasts. A stream injection usually labels stream transport storage rather than an entire catchment-connected aquifer. The ideal mass source in this proof must not be equated with that field procedure.

The model excludes spatial mixing, bypass flow, additional stores, unknown sorption, changing evaporation endmembers, and unmeasured tracer sources. The noise study excludes correlated errors, concentration bias, uncertain Q and uncertain dose delivery. It tests one smoother, one forcing design and one storage history. More realistic models or estimators can change both identification and precision. Full rank is sufficient within this model, not a guarantee for a heterogeneous catchment. The result provides a testable method to reduce a known attribution ambiguity; it does not resolve the physical cause of the regional runoff loss or propose catchment-wide dosing.

## Reproduce and inspect

Extract the verified ZIP. Use Python 3.12 with NumPy, SciPy, pandas and matplotlib. From the extracted publication root run:

    python files/analyze.py /absolute/path/to/separate-output
    python files/audit.py /absolute/path/to/separate-output

Both scripts reject output inside the publication. The first takes seconds and regenerates all 3,609 runs, exact inputs, summary and figure. The second independently checks triangular reconstruction, rank loss, integrated balance and the post-injection scale alternative. It saves the two integrated water and mass trajectories. Bundled results permit inspection without a rerun. Package versions and seed are in files/results/summary.json. No network, external dataset or private scratch is needed to reproduce any numerical claim.

No shared dataset was used. The exact shared paths, full ZIP hashes and used text-member hashes of prior SCI publications are in files/provenance.json. External papers are cited, not bundled. All code, text, figures and synthetic outputs in this package are original to this job and eligible for the SCI baseline terms. files/DATA_NOTICE.md explains this scope.

Job: sci-1107-dell-earth-and-ocean-sciences-8fd5ea292bb5. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort through Codex in T3 Code. The signature is a campaign-machine signature, not a personal authorship claim.
