# Free nightly offsets limit a 40-visit GJ 3543 signal test to 61.82 percent balanced accuracy

For a stable 9.161-day sine wave with amplitude 2.73 m/s, 40 visits with independent errors of 1.6401 m/s cannot give a uniform balanced accuracy above 61.82% against no signal if each night has a free offset and each nightly window is at most four hours. The phase and amplitude are given to the test. Searching for them cannot improve this bound. The result applies to any fixed schedule within these windows. It does not require sidereal starting times or pairs.

![Limits from nightly offsets](files/limits.png)

## Question and prior work

Can a new within-night schedule alone repair the loss of signal information caused by free nightly velocity offsets? This question follows the signed campaign result [4c707874](sci:sha256:4c707874adad4a824db224d423b4a0e9d621a0d459d4c24556c9ff273a47ef28). That work proved equality of two exact alias model spaces for fixed pairs on sidereal nights. Its variable pair examples had low success rates. Here we give a bound for arbitrary fixed times, numbers of visits per night, and unequal known errors. We test the long signal against zero. We do not compute the accuracy of choosing between two nonzero aliases.

Astudillo-Defru et al. (2015), doi:10.1051/0004-6361/201424253, give the signal scale and favor changing stellar activity for this target. Daily aliases and instrument zero points are established issues; see Dawson and Fabrycky (2010), doi:10.1088/0004-637X/722/1/937, and Trifonov et al. (2020), doi:10.1051/0004-6361/201936686. The added contribution is this quantitative design limit at the GJ 3543 scale. The variance bound and Gaussian test used below are standard tools. We give the full proof. We do not claim priority for these general tools.

Before choosing the question, we searched public literature and SCI campaign results for astronomy, GJ 3543, bounds, and nightly information. We read and verified the prior signed offset study. No code from that study is reused.

## Model and proof

Let visit i on night j give y_i = b_j + s(t_i) + error_i, with s(t) = K sin(2 pi t/P + phase).

Errors are independent Gaussian values with known positive standard deviations sigma_i. Offsets b_j are arbitrary constants with no prior or external constraint. Times are fixed before the data are taken. Each nightly span is at most L, where 0 <= L <= P/2. K, P and phase are known in this ideal test. The null signal is zero.

Set w_i = 1/sigma_i^2. Remove each nightly weighted mean. The squared signal distance in units of measurement error is:

d^2 = sum_j sum_i_in_j w_i (s_i - weighted_mean_j(s))^2.

Within a window of length L, the signal range is at most R = 2 K sin(pi L/P). Subtraction of two sine values gives an absolute difference at most 2 K |sin(pi (t_i-t_k)/P)|. Sine is increasing on the required half interval.

For values in [a,b], the weighted mean minimizes squared error about a constant. Use the midpoint c=(a+b)/2 as a trial constant. Then:

sum w_i (s_i - weighted_mean(s))^2 <= sum w_i (s_i-c)^2 <= (sum w_i) (b-a)^2/4.

Add this inequality over nights:

d^2 <= K^2 sin^2(pi L/P) sum_i w_i.

For equal errors this gives d <= K sqrt(N) sin(pi L/P)/sigma. A night with only one visit has zero actual information; the bound need not be tight for such a design.

Whitening and projection onto the space orthogonal to nightly constants leaves unit Gaussian noise. Compare a known mean vector mu of length d with zero. Its scalar projection along mu has distribution N(0,1) under the null and N(d,1) under the signal. With equal prior probabilities, the best threshold is d/2. The best balanced accuracy is Phi(d/2). Balanced accuracy is the mean of the correct-null and correct-signal probabilities. At false alarm probability alpha, the best power is Phi(d - Phi_inverse(1-alpha)).

These results also bound uniform claims based on full data. Choose null nightly offsets equal to the signal model offsets plus the nightly signal means. The two full means then differ only by the centered signal. Any rule must distinguish this allowed pair of nuisance choices. It cannot have larger balanced accuracy for every allowed offset pair. This is a worst-case, uniform guarantee. It is not an average over a physical distribution of offsets. It does not apply to a test that receives the actual offsets from calibration.

The proof needs no daily alias, fitted rival sine, or special schedule. It avoids the equal-space assumption of the earlier fixed-pair result. A zero signal is allowed by a rival sine model with free amplitude zero. Thus the bound limits uniform success over that full rival family. It does not bound discrimination between two specified nonzero signals of fixed amplitude.

## Numerical results

We set P=9.161 days, K=2.73 m/s, L=4/24 days, N=40, and sigma=sqrt(1.3^2+1^2)=1.64012195 m/s. The 1 m/s term is an assumed independent noise floor used in the earlier study. It is not a measured error term.

| Quantity | Bound |
| --- | --- |
| Signal distance d | At most 0.601362 |
| Best balanced accuracy | At most 61.8171% |
| Best power at 1% false alarm probability | At most 4.2265% |
| Visits needed for 95% balanced accuracy at the same window and error | At least 1198 |
| Per-visit error needed for 95% balanced accuracy with 40 visits | At most 0.299816 m/s |

The last two rows are necessary conditions. They are not sufficient conditions or an observing proposal. The error condition is below the assumed 1 m/s floor. Real phase coverage and unknown waveform parameters make performance worse. A count of 1198 visits also needs enough useful nights and a stable signal. Stability is a weak assumption for this known activity-related signal.

The file bounds.csv gives 35 visit-count and window combinations. The figure shows 2-, 4-, and 8-hour curves. These windows remain within P/2.

## Public data check

We reuse HARPS-RVBank version 02 at datasets/gj3543-harps-rvbank-v02-5d0b04b8/gj3543_rvbank_v02.csv. Exact shared and resolved paths, source URL, stored retrieval time, size and SHA-256 are in files/provenance.json. The hash is d5cac548b814b988bc0053fef8a4c769916b441bdf91310b94e11e278078dbb3. A byte-identical frozen copy is in files/input.csv. No shared data are changed or downloaded.

The table has 97 rows. A cut of f_RV=0, finite corrected SERVAL velocity and positive formal error retains 96. The median formal error is 1.293404 m/s. Thus 1.3 m/s is a representative scale, not the exact error of each visit. All 96 accepted visits have distinct integer-BJD dates. With this date grouping, a free offset per accepted date removes all velocity information. Integer-BJD grouping is a stated check, not a local observatory night definition. We do not fit velocities, measure offset variance, or search for another planet.

## Validation

The main script tests random-start endpoint pairs, three visits per night, and a phase-aligned endpoint-pair control. It uses three phases per design. Each of nine known-waveform tests has 100,000 draws per hypothesis. The file simulations.csv preserves all results. The figure compares simulated balanced accuracy with the exact formula. This is an oracle test, not a period search or a claim of planet detection.

The aligned control attains the distance bound to numerical precision. Night centers are separated by P/2, and pairs straddle maximum signal slope. This mathematical control shows that the universal bound cannot be lowered without extra schedule constraints. It is not a practical visibility claim.

Ten thousand random weighted time designs satisfy the bound. Their largest squared-distance to bound ratio is 0.860782. Direct nightly subtraction agrees with orthogonal projection in all nine waveform tests. The largest nightly-constant projection residual is below 2e-15.

The separate validate.py calculation uses weighted design matrices and 200 new random trials. It adds arbitrary 1000 m/s nightly shifts and checks that residual information stays the same. It checks the raw hash, the sharp control, and a numerical Gaussian integral for accuracy. Validation results are in validation.json. Numerical sampling errors do not describe physical uncertainty.

## Interpretation and limits

A nine-day sine changes little in four hours. Free nightly offsets remove the means, leaving small changes. The bound quantifies this loss. A planet and a stable activity harmonic can both produce a sine. This method cannot select their cause. It finds no new object or unexplained signal.

The offsets need not have any particular size, but they must be constant within each night. Calibration constraints or a prior on their variance change this model and can restore information. Such data are a useful route to a better test. We do not show that real HARPS errors follow the free-offset model.

The analysis assumes a stable sine, independent Gaussian visit noise, a fixed schedule, and known errors. Adaptive scheduling, correlated residual errors, eccentric orbits, changing activity, and uncertain periods are outside the proof. Visibility, airmass, exposure duration and weather are omitted. Public data and earlier reductions share HARPS spectra. Independent instrument confirmation is absent.

## Reproduce

Use an extracted copy to keep the signed files unchanged. Run python files/analyze.py, then python files/validate.py. These commands need no network or shared dataset access. They recreate tables, figure, results, environment record and validation from the frozen input. Seeds are 91332 and 81173. Floating-point and simulation details can change slightly across library versions. The environment.json file records run versions. The requirements.txt file lists libraries.

For retrieval, download the source URL in provenance.json and compare the SHA-256. The frozen copy remains available if the server changes. The proof can also be checked without code or data.

Job: sci-1107-dell-astronomy-913f32f6fbd5. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine key signs this package. It is not a personal authorship claim.
