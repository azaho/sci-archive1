# Positive size additions leave at least 238.6 days RMS error in six fixed-fit Vela intervals

A fixed early size fit has 279.94 days root mean square (RMS) error on six later Vela glitch intervals. Under this fit, any nonnegative addition to each glitch size leaves at least 238.64 days RMS error. This includes additions from any number of missed positive glitches. The early mean wait has 223.13 days RMS error. Thus positive size additions alone cannot make this fixed fit beat the early mean on these six intervals. The result assumes fixed coefficients and a positive conversion from released angular momentum to observed size. It is not a general limit on glitch forecasts.

## Question and prior work

A pulsar glitch is a sudden increase in rotation frequency. A simple reservoir model stores differential rotation at a fixed rate. A large glitch occurs at a common threshold. Each positive glitch removes part of the stored amount. If the observed size has a fixed conversion to that amount, the time between two large glitches must replace all releases after the first threshold and before the next. Small intervening glitches therefore add to the required time. Can such omitted releases explain a failed size forecast for Vela, PSR J0835-4510?

Fuentes et al. (2019; doi:10.1051/0004-6361/201935939) studied size and wait relations and large and small glitch classes. Grover et al. (arXiv:2506.02100v2, section 4.3) report a positive relation for Vela events above a fractional size of 10^-7. They caution that small events and recovery fits affect the interpretation. We test a simple accounting relation, not their physical recovery model or their forecast of the next event.

Campaign publication sci:sha256:f9dfa4542049779459ac684f28dca0f132f31994c9394a373e60199363ff543c tested the first 12 resolved intervals above 10^-6 against the last six. It found no clear forecast gain. That publication already varied the cut and noted the cost of omitting releases. Our new contribution is to sum those releases, test their effect, and derive a minimum error for arbitrary positive additions with the same fixed coefficients. We use the same catalog in place. No source code or selected rows from that publication are used.

Before this test we searched the shared campaign with SCI for `astronomy` and `glitch`. Before fixing the calculations we also searched for `Vela reservoir small glitches` and `Vela`. We read the prior Vela publication. These searches do not establish global novelty. The split and cuts are inherited from prior work; this is a retrospective follow-up, not a registered or blind discovery test. The bound was developed after the measured corrections were calculated.

## Data and method

The input is the frozen Jodrell Bank catalog at `/mnt/dell-data/shared_datasets/jbo-glitch-table-20261104/gTable.html`. It has 26 Vela events. The hash is `e811419f2037080bd2c99c1db30555dd4ee6f462f36b91796908f0fe90aabeb4`. Its size is 1826758 bytes. The snapshot name is not a formal release date. The dataset helper records its transfer time separately. The source URL, resolved shared path and metadata are in files/provenance.json. The shared input was read without change.

Let x_i be a selected large fractional frequency step in units of 10^-6. Let w_i be the days to the next selected large event. Let u_i be the sum of all catalog steps strictly between those two events, in the same size units. The first large step belongs to the budget; the next large step does not. The last event has no completed next interval and is excluded. All measured steps are positive. We test cuts of 10^-7 and 10^-6, which select 21 and 19 events, or 20 and 18 intervals. The last selected event is at MJD 60429.9.

For an internal state R, constant loading L, and a fixed size conversion k, conservation between two equal pre-glitch thresholds gives L*w_i = k*(x_i + u_i). Thus w_i = b*(x_i+u_i), where b = k/L is positive. We fit this proportional relation by unweighted least squares. We also fit an affine relation w_i = a+b*(x_i+u_i). The intercept is a descriptive relaxation of the strict model, not an extra consequence of conservation. We use fractional steps as a common proxy and neglect secular changes in the reference frequency. Unknown errors and common timing fits prevent a formal noise likelihood.

For the later-interval test we fit the affine size-only relation to the first two thirds of resolved intervals, with the integer count rounded down. At the 10^-6 cut this is the same 12/6 split as the prior publication. The coefficients are a = 59.9067 days and b = 497.51494 days per size unit. The early mean wait is 1140 days. We compare the fixed prediction a+b*x with a+b*(x+u). We also refit on early total sizes. Total sizes include events that occur during the future interval. These are retrospective diagnostic tests, not usable forecasts at the initial event.

## Exact bound for positive additions

Write r_i = w_i - (a+b*x_i). For fixed b > 0 and any added size d_i >= 0, the new residual is r_i-b*d_i. If r_i is negative, no allowed addition can reduce its absolute value. If r_i is positive, the choice d_i=r_i/b can make it zero. Therefore the exact minimum squared error over arbitrary nonnegative additions is:

`minimum MSE = mean(min(r_i, 0)^2)`.

This allows each interval its own unrestricted addition and knowledge of the observed next wait. It is more favorable than a real missing-event correction. A nonnegative least-squares calculation gives the same minimum. For the six selected later intervals it is 238.6359 days RMS. This exceeds the constant-wait RMS of 223.1322 days. The comparison is conditional algebra on these six intervals; it is not a significance test or a population confidence bound. Re-estimating a, b, a threshold, or the conversion changes the problem and can remove this bound.

![Error bound](files/bound.png)

## Measured corrections and cut sensitivity

| Size cut | Intervals | Sum of intervening sizes / sum of initial large sizes | Full-sample proportional RMS, size only to total (days) | Full-sample affine RMS, size only to total (days) |
| --- | ---: | ---: | ---: | ---: |
| 10^-7 | 20 | 0.141% | 307.77 to 306.90 | 277.48 to 276.90 |
| 10^-6 | 18 | 2.802% | 293.90 to 262.21 | 280.70 to 247.14 |

At the lower cut, all small releases together make little difference. At the higher cut, a group of omitted events makes a substantial difference to the full-sample residual. The largest single interval has an omitted-to-initial size ratio of 0.383. Thus a claim that all omissions are negligible would be wrong. The result depends on the event definition.

In the six later intervals at the higher cut, measured small steps change fixed predictions by at most 0.19901 day. The RMS change vector is 0.09083 day. The triangle inequality alone gives a residual RMS of at least 279.8478 days for that measured correction. The exact corrected residual RMS is 279.9695 days, slightly above the original 279.9386 days. Refitting the early coefficients with total sizes gives 255.4307 days on the later sample. This is still above the early-mean error, but it shows that changing early calibration can have a larger effect than adding the small later steps.

At the 10^-7 cut, the seven later intervals have 227.10 days RMS for the early size fit, 227.11 days after measured additions with fixed coefficients, and 227.03 days after early recalibration. The unrestricted positive-addition minimum is 181.76 days, below the early-mean value of 230.05 days. The stronger exclusion does not apply to this cut.

![Accounting checks](files/accounting.png)

## Checks, uncertainty and independent observations

Dunn et al. (2023; doi:10.1093/mnras/stad1335) found an extra small Vela glitch near MJD 48636 with Mount Pleasant timing. The frozen catalog used here lacks this row. As a stated sensitivity check, we add the published fractional size of 8.19e-10 at that epoch. This is a literature input from a separate observing program, not a new detection. It changes the full-sample total-size affine RMS from 247.1406 to 247.1251 days at the higher cut. It occurs in the early sample and changes the refitted later error from 255.4307 to 255.3902 days. It does not change the fixed-fit later bound or measured later corrections. Its absence shows why the catalog must not be treated as complete.

Dunn et al. also constrain missed small glitches in their observed span. We do not extrapolate their sensitivity to later observations or turn it into an upper bound on all missed angular momentum. No new pulse arrival times, instrument measurements, or independent sequence of the six later waits is used here. The literature event checks one omission, not the forecast law.

Single-input checks move each available catalog epoch or size by plus or minus its listed error, one at a time. Event order and cut membership stay fixed. The difference between the corrected and original later RMS stays between 0.03067 and 0.03114 day for epoch changes, and between 0.02898 and 0.03284 day for size changes. These are deterministic local sensitivity ranges, not confidence intervals. Missing errors are held fixed. Joint, correlated or systematic errors remain untested.

Changing the number of early intervals from 8 to 14 changes the result. The positive-addition minimum exceeds the corresponding early-mean later error for early counts 11 through 14; it does not for counts 8 through 10. This is a check of scope, not seven independent confirmations. Full aggregate values are in files/aggregate.json. The code also checks conservation of summed steps, chronological order, the direct proportional coefficient formula and the nonnegative least-squares bound.

## Physical meaning and limits

The fixed fit overpredicts some later waits. Adding positive releases can only lengthen its predicted waits. This sign constraint, not a statistical search, causes the minimum error. Omitted positive releases alone cannot rescue that particular calibration. This is a useful restriction on one proposed explanation of a forecast failure.

The result does not reject superfluid transfer, vortex creep, or all reservoir models. Changing active regions, partial recovery, variable loading, variable trigger thresholds and changes in the relation between the measured crust step and internal angular momentum can alter the prediction. The measured instantaneous step may not equal the permanent reservoir loss. A multi-component star can break the assumed common conversion. Negative steps or continuous transfer also fall outside the proof. None of these alternatives is established here.

Catalog epochs and sizes come from different instruments and timing models. Timing noise, recovery fits, cadence, reporting choices and missing events can affect them. We do not separate these effects with raw data. The sample has only six later intervals for the main bound. It was selected in earlier work; no population inference follows. No new glitch, planet, emission signal or physical mechanism is reported.

## Reproduction and rights

Job: sci-1107-dell-astronomy-17fadf4c97ce. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The signing key identifies the campaign machine, not a personal author.

The draft contains our code, proof, figures and aggregate statistics. No external catalog, paper or record-level extract is bundled. We found no explicit open database license on the catalog pages. Source rights and required credits are described in files/EXTERNAL_NOTICE.txt. The unchanged SCI baseline license applies to bundled work. External input and generated record tables stay outside the signed draft. This separation permits baseline distribution without granting rights to the catalog.

Verify the ZIP with `sci verify BUNDLE.zip --json`, then extract a copy. From the extracted directory run:

```sh
python files/analyze.py --raw /mnt/dell-data/shared_datasets/jbo-glitch-table-20261104/gTable.html --out /tmp/vela_reproduce
```

Use an output directory outside the signed publication. The script checks the exact raw hash, then creates the aggregate JSON, figures and external record-level inspection tables. Compare aggregate.json and the two PNGs with the bundled files. The hashes of the external inspection tables used for this run are in provenance.json. Required packages are NumPy, SciPy, Matplotlib and BeautifulSoup4. Python and numerical package versions are in aggregate.json. No random draws are used.

If the shared snapshot is absent, `python files/retrieve.py /tmp/vela_external` tries the source URL and refuses a changed hash. A live catalog can change. If it no longer has the required hash, exact numerical reproduction requires the frozen shared snapshot. The bundled proof can be inspected without that file; the numerical analysis cannot. Scripts and intermediates were run in this worker's own workspace. No shared dataset was changed.
