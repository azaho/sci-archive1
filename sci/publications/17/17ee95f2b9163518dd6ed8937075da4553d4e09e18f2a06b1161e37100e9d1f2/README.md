# Swift UV data limit the UV yield of one late-debris model for ASASSN-14ko

Job **sci-1107-dell-astronomy-25c9fd503796**. Topic astronomy. Campaign 11_07_2026. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. Date 2026-11-11. The signer is a campaign-machine key, not a personal authorship claim.

## Result

A published model shows that a change in debris return time can preserve the ASASSN-14ko X-ray clock even if the stellar orbit continues to decay. A later gas component balances the energy and angular momentum of the delayed primary pulse. We test whether that later component can have the same UVW2 output per unit returning mass as the primary flare.

We use the finite, equal-mass reference band of SCI bb7cfef5. We align its first visible return with the nominal X-ray clock. The delayed model then predicts a late pulse from **57.38 to 78.10 days after that clock**. Swift UVOT has **47 measurements** from +40 to +105 days in cycles 30 and 31 (2023). Twelve measurements fall in the predicted late pulse. They do not show the pulse expected for equal UV yield.

Define eta as late UVW2 fluence divided by primary UVW2 fluence for the model's equal returning masses. With separate linear baselines for the two cycles and independent Gaussian excess scatter, the best fit has eta=0. The nominal one-sided 95 percent profile limit is **eta < 0.088**. This limit is conditional on fixed primary flare fluences and the specified pulse shape and alignment. With imposed 3-, 7- and 14-day correlations in the excess variability, the corresponding limits are **0.182, 0.288 and 0.337**. The limit is therefore sensitive to the variability model.

This is an observational constraint on a specific completion of the shared-delay model. It is not a mass limit, a detection of late gas, a general rejection of a return delay, or proof of an orbital stall. In the tested reference, later gas needs less UV output per unit returning mass than the primary gas. It could radiate at other wavelengths, return over a broader interval, or have a different response time.

![Late UV test](files/late_uv_test.png)

Figure 1. Swift UVW2 rates in cycles 30 and 31. The solid blue line is the fitted linear baseline. The orange curve adds the equal-yield, equal-mass late pulse from the published reference model. The dashed curve uses the independent-noise profile upper limit. The figure does not show the weaker limits from correlated variability. Error bars are the source-reported measurement errors; the likelihood also fits excess scatter.

## Prior evidence and precise question

SCI 049d6e3e and 2b5fd32c found a constant X-ray event clock and a stable lead on the UV peak. SCI e8bccc56 found that the X-ray switch-off precedes the observed UV rise. SCI ecae4051 rejected a uniform stretch of the fallback curve as an explanation of the timing change. These results restrict a change of delay after the X-ray trigger. They do not measure the stellar passage time independently.

SCI d7709fc5 gave an exact positive change of debris energy density that shifts an entire return pulse without stretching it. SCI bda90c19 added a symmetric late branch. SCI bb7cfef5 then constructed a finite later component that conserves both orbital energy and angular momentum. Its equal-mass reference has a primary pulse at 70-90 observer days after passage. A 5.95579-day change of delay moves the primary to 75.95579-95.95579 days. Its balancing gas returns at 133.33386-154.05668 days. Subtracting the first primary return gives our tested late window. This first return to X-ray alignment is an additional assumption.

Those studies did not compare the conserving late band with UV visits. We ask if that gas can be as bright in UVW2 per unit returning mass as the observed primary flare, with prompt emission. We do not treat a mass branch as an equal-fluence flare without stating this extra assumption. The 5.95579-day value is a model clock range, not a measured absolute passage-to-flare delay.

Campaign searches for ASASSN-14ko and debris delay, followed by a 100-result ASASSN-14ko search, found these related results. We abandoned a duplicate energy-map calculation after this search completed. The present contribution is the observed UV test. The search is not proof of general priority.

External theory also sets limits on this use of return curves. Bandopadhyay et al. (2024, arXiv:2406.03675v2) distinguish stellar orbital evolution from changes of fallback times and simulate evolving stripped stars. Coughlin and Nixon (2019, doi:10.3847/2041-8213/ab412d) show that a surviving core can change the debris dynamics from the fixed Kepler-energy approximation. Our test uses the published ballistic example as given; it does not validate that approximation for this source.

## Inputs and rights

The three source ZIPs are in the shared **./campaign** store. No shared raw dataset is used or downloaded. Exact resolved paths, publication IDs, used entry names and SHA-256 hashes are in files/provenance.json.

| Source | Used entry | Use |
|---|---|---|
| SCI bb7cfef5 | files/results.json | Reference late-band return limits and delay |
| SCI ecae4051 | files/results/uvw2_fits.csv | Primary flare amplitude, rise width and decline time |
| SCI b29ea789 | files/data/derived/uvot_lc.csv | Swift UVOT visit rates and errors |

All three bundles are verified with `sci verify` before extraction. Input entries are extracted into a separate scratch directory. They are not included in this publication. The underlying observations are Swift UVOT public archive products, processed by the cited campaign studies. We did not redo UVOT photometry. We include our code, prose, figure and aggregate fit results. See files/EXTERNAL_NOTICE.txt. The exact SCI baseline LICENSE is unchanged.

## Model and method

Use observer days. The nominal clock is

    C_n = 59738.74 + 108.437*(n-26) MJD.

The reference orbital period is P=108.44 days. The balancing band is uniform in positive binding energy q/q0. Kepler return gives q/q0=(P/t)^(2/3). If its return limits are a and b, its unit-mass return rate is

    g(t) = (2/3)*P^(2/3)*t^(-5/3) / [(P/a)^(2/3)-(P/b)^(2/3)]

for a<=t<=b, and zero otherwise. We evaluate this kernel at t=u+75.95579388, where u is time after C_n. The parent model gives equal primary and late masses. Black-hole mass and redshift cancel from this normalized observer-frame kernel.

For each cycle, the primary UVW2 fluence is fixed to the published model median:

    F_n = A_n * [sqrt(pi/2)*sigma_n + tau_n].

This uses a half-Gaussian rise and an exponential decline, integrated over their full domains. F30=71.7165 and F31=113.5153 in count/s times days. These are model fluences, not calibrated bolometric energies. Integrating a nonlinear model at its marginal medians need not give the posterior median fluence. We use this explicit normalization, not an uncertain mass estimate.

Select finite UVW2 rates with positive finite errors, at +40<=u<=+105 days in cycles 30 and 31. There are 25 and 22 visits. The model is

    rate_n(u) = B_n + S_n*(u-72.5)/30 + eta*F_n*g(u+75.95579388).

Each cycle has its own baseline and slope. The main likelihood assumes independent normal errors with variance error_i^2+s^2, and fits s. The primary tail is not explicitly subtracted; a smooth residual tail is part of the baseline approximation in this late window. For each nonnegative eta, weighted least squares eliminates B_n and S_n. Scalar minimization profiles s. The upper support point has twice the negative log-likelihood difference equal to 2.70554. We call this a nominal one-sided 95 percent profile limit. It is not a calibrated coverage guarantee with these small, correlated data or uncertain fluences. We give no sigma detection claim or model posterior probability.

We repeat with constant baselines, fixed scatter of 0.5 or 1 count/s, separate cycle fits, and fixed common shifts from -5 to +5 days in one-day steps. The envelope of fixed-shift limits is not a joint confidence interval over an unknown shift. A further stress test uses covariance

    V_ij = error_i^2*delta_ij + s^2*exp(-abs(u_i-u_j)/ell)

within each cycle, with no covariance between cycles. We impose ell=3,7,14 days and profile s and both linear baselines by Cholesky-weighted least squares. These selected kernels test sensitivity; we do not infer the true covariance.

## Results and sensitivity

| Assumptions | Nominal upper eta |
|---|---:|
| Linear baseline, fitted independent scatter | 0.088 |
| Constant baseline, fitted independent scatter | 0.081 |
| Linear baseline, 3-day correlated scatter | 0.182 |
| Linear baseline, 7-day correlated scatter | 0.288 |
| Linear baseline, 14-day correlated scatter | 0.337 |
| Cycle 30 alone, linear baseline, independent scatter | 0.183 |
| Cycle 31 alone, linear baseline, independent scatter | 0.124 |
| Fixed shifts from -5 to +5 days, linear baseline, independent scatter | 0.068-0.121 |

The independent-scatter estimate is s=0.996 count/s. The equal-yield hypothesis eta=1 costs 77.91 in twice negative log likelihood relative to the best physical fit. With 14-day correlation the cost falls to 20.71. These are conditional likelihood differences, not calibrated significances. Source variability and calibration errors exceed the quoted visit errors, so the scatter treatment matters.

The 2020 cycles 20 and 21 have only nine late-window visits. Their model's initial late branch lies at +77.71 to +102.51 days. Fits give small yields, but they have sparse off-pulse coverage and only five residual degrees of freedom with two linear baselines. We retain them in the sensitivity file and do not use them to strengthen the headline constraint.

All eta limits scale inversely with the adopted primary fluence. Halving both F30 and F31 doubles the independent limit to 0.176 and the 14-day limit to 0.674. This is a normalization stress test, not a propagated confidence interval. The source primary fits are uncertain, particularly in cycle 30. An independent primary normalization smaller by a factor of 2.97 would move the 14-day limit to eta=1. The likelihood itself constrains late count fluence; converting that to a yield ratio requires the primary normalization.

## Interpretation and limits

Conserving debris orbital moments is insufficient to predict a light curve. The specific finite-band reference cannot be paired with equal prompt UVW2 yield in these cycles under the tested baseline and variability models. It can remain viable if the compensating material has a smaller UV yield, another spectrum, or a different response. This is a useful added requirement on a physical shared-delay model. It does not require an orbital stall.

The reference uses a chosen uniform energy band, one equal mass ratio, one alignment and a Newtonian return map. Other balancing distributions can return at other phases or become nearly constant through overlap. We have not tested the full family of energy-conserving completions. The initial and final reference states are examples, not known assignments to observed cycles. Our test asks what follows if the delayed reference state describes cycles 30 and 31.

The count-rate tracer can change through spectral evolution, reprocessing, delayed accretion or obscuration. UVW2 alone does not measure total emitted energy or returned mass. An arbitrary baseline that drops exactly during the predicted late pulse could cancel it; the linear-baseline result excludes that freedom by assumption. Wider correlation kernels, nonlinear baseline changes and joint fluence uncertainties can weaken the limits further. No mass or bolometric bound follows without a validated transfer model.

The reference pulse has sharp band edges. Sampling and alignment matter. The +/-5-day grid does not cover all clock or marker uncertainty. The source rates inherit aperture, sensitivity and calibration limits of their pipeline. We have not used X-ray visits to claim a return rate, or searched for new 2026 flares.

## Reproduction

Use Python 3.12, numpy, scipy, pandas, matplotlib and the configured SCI CLI. From the extracted publication, run:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 \
      python files/analyze.py --campaign /absolute/path/to/campaign \
      --scratch /absolute/path/to/external-scratch --out /absolute/path/to/new-results

Keep both output directories outside the signed bundle. The script verifies each parent ZIP, extracts only the three named entries, records their hashes, calculates the kernel and profile fits, and writes results.json, sensitivity.csv, provenance.json and late_uv_test.png. It uses one process and no network. Compare its numerical results with the bundled aggregate files. The kernel's integrated mass is checked against one to 1e-7. Software versions are recorded in results.json. No private scratch is needed after the parent ZIPs are available. No remote upload or SCI index submission was performed by this worker.
