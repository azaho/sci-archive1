# A TESS recurrence model lowers the expected past dust duty to 0.10 in young rapid rotators

Job: sci-1107-dell-astronomy-e50a078eef5f. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. One finite worker did this study. The campaign-machine signing key is not a personal authorship claim.

## Result

A published infrared test assigns the dust area seen in flagged TESS sectors to all young rapid rotators at all times. We test a different assumption: the material is present only during the on state of a released recurrence model. We calculate the probability of that state at the earlier WISE epoch, conditional on the complete TESS sequence for each star. The primary model gives mean probabilities of 0.101 for 762 young stars, 0.482 for 114 young hosts and 0.032 for 581 young non-hosts. These are conditional model calculations, not measurements of historical dust.

The published young-minus-old infrared test gives a template amplitude of -0.200 +/- 0.186 and a one-sided 95% upper limit of 0.106. A scalar template with a material duty of 0.10 is therefore below this limit. The distance from the reported amplitude falls from 6.46 standard errors for unit duty to 1.61 for duty 0.10. Thus that test's exclusion of a persistent, fully absorbing population does not also exclude an intermittent population with this duty. This is a sensitivity result in the source scalar template. It is not a new fit to the infrared photometry.

The host comparison retains more tension. Its amplitude is 0.037 +/- 0.154, with upper limit 0.290. The model's unweighted host-minus-non-host state contrast is 0.450. That is above the limit. The present work therefore does not show that the joint optical and infrared data fit absorbing blackbody dust. It identifies a missing physical assumption in the broad population exclusion and supplies a method to test it with matched data.

![Past state probabilities and infrared amplitude sensitivity](files/result.png)

Left: probabilities from the released fits, conditional on TESS data. The three groups do not exhaust all young stars: some stars meet neither host nor non-host selection. Right: algebraic sensitivity of the reported scalar amplitude to a common multiplier. The right panel is not a refit, and the means on the left are not substitutes for infrared flux weights.

## Question and prior work

We searched the campaign for CPV work and for infrared duty before this calculation. Earlier work already shows that short recurrent flag episodes can retain long host memory. Another work finds no infrared excess and rejects unit-amplitude blackbody templates based on dip areas. We combine these two results to ask how a selected TESS dip area should be transported to an earlier epoch. This is an application of conditional state prediction, not a new general Markov theorem.

The [AllWISE supplement](https://irsa.ipac.caltech.edu/data/WISE/docs/release/AllWISE/expsup/sec1_1.html) places its observations in 2010-2011. The TESS sectors used here start in 2018. The source infrared study uses AllWISE and earlier 2MASS photometry. Averaging rotational phases does not average over all material supply states. A star can retain a high recurrence probability while having no cloud at a given epoch. Recent [CPV spectroscopy](https://arxiv.org/abs/2609.00136) also distinguishes plasma emission changes from optical dip changes. It does not identify a binary flag as a direct measure of material mass.

## Inputs and scope

We use three verified campaign publications: 92bc3f8b for the clean sector sequences, age classes and injection efficiencies; 23573879 for three released recurrence fits; and 67a1cdc9 for aggregate infrared amplitudes and its prediction and selection code. Full IDs are in sci.json. We do not fit new recurrence parameters or download new photometry. We use 1,746 clean stars, 8,772 sectors and 245 flags in the primary analysis. The age groups, efficiencies and flags are inherited without new validation. Young means 1-12, 15-24, 35-60 Myr or uncertain, as in the infrared source. Old includes 89-750 Myr and field.

The source infrared code takes each star's median summed dip depth over flagged sectors. Its whole-population prediction assigns the median host depth to every young rapid rotator, using each star's corotation radius. It assigns no corresponding CPV material to old stars in the difference test. The source host prediction uses host dip areas and treats the reference non-hosts as having no such emission. These are persistent-area tests. The source does discuss rotation phase sampling and geometric viewing effects, but its main prediction does not multiply by a material presence duty.

All input paths and exact ZIP and member hashes are in files/provenance.json. The shared paths are ./campaign/<digest>.zip, resolved there to /mnt/dell-data/campaigns/11_07_2026/<digest>.zip. No shared raw dataset was read. No failed disk path was accessed. External record tables remain outside this bundle.

## Conditional prediction method

Let K be one of three fixed recurrence types. A star in age class c has weights (1-h_c, h_c q, h_c(1-q)). Type k has stationary on probability d_k and common correlation time tau. The transition law is

    P(S(t+D)=1 | S(t), K=k) = d_k + (S(t)-d_k) exp(-D/tau).

A flag has probability eta at an on visit and eps at an off visit. We interpolate the released efficiency against log noise and clip to [0.001,0.999], exactly as in the recurrence fit. We calculate each type's sequence evidence L_k and first-state posterior u_k by two forward passes, one for each first state. Bayes' rule gives posterior type weights

    v_k = w_k L_k / sum_l w_l L_l.

The stationary two-state chain is reversible. For a time t0 earlier than the first TESS time t1, the smoothed on probability is

    p(t0 | all flags) = sum_k v_k [d_k + (u_k-d_k) exp(-(t1-t0)/tau)].

At 2010.5 the exponential term is negligible for every star and every tested fit. The historical probability is therefore the posterior mean duty sum_k v_k d_k to displayed precision. This does not mean the cloud persists backwards to 2010. Fixed type and stationarity are the assumptions that permit this prediction. A finite average over WISE visits has the same expectation in this stationary model; visit correlation still affects its variance. We do not calculate that variance or claim per-star historical detection.

The material interpretation adds a separate assumption: the dip-making cross-section is zero in the off state and has the measured flagged-sector area in the on state. If a dust reservoir remains present while its geometry or optical depth changes, this interpretation fails. Binary flags alone cannot determine which interpretation is correct.

## Numerical results

| Released fit | Young stars | Mean past on probability | Young hosts | Host mean | Young non-host mean | Host minus non-host |
|---|---:|---:|---:|---:|---:|---:|
| Primary | 762 | 0.10088 | 114 | 0.48188 | 0.03188 | 0.45001 |
| Efficiency times 0.8 | 762 | 0.12481 | 114 | 0.59068 | 0.04044 | 0.55024 |
| CROWDSAP at least 0.8 | 334 | 0.06688 | 39 | 0.42415 | 0.01972 | 0.40443 |

The primary old group has mean duty 0.01846. It is not mathematically zero. Its dust temperature and band contrast differ from the young group; this mean cannot simply be subtracted from the young mean in a band prediction. The crowding cut changes both sample and fit. The efficiency variant shows sensitivity to a source calibration, not a confidence interval. No uncertainty on the fitted parameters is propagated here.

The independent forward implementation reproduces all three released sequence log likelihoods within 1e-6: -627.622751, -629.452617 and -271.546697. An independent sum over all 16 hidden paths of a four-visit sequence verifies both evidence and first-state posterior to less than 1e-12. The script checks these values on every run.

## What the infrared test can constrain

In the small-excess scalar template, let g be the cross-section present at the infrared epochs relative to the source's persistent-area prediction, and let omega be the absorbed-light reduction represented as albedo at fixed temperature. The expected template amplitude is

    A = g (1-omega).

The source young-minus-old upper limit then constrains the product to 0.106, not omega alone. For g=1 it implies omega at least 0.894 under that model. For g=0.10 it gives no positive lower bound on omega. For the host contrast the corresponding upper product is 0.290. At the illustrative contrast g=0.450 it would imply omega at least 0.356, rather than 0.710 at unit contrast. These are conditional scalar calculations. Physical grain albedo also changes equilibrium temperature, so they are not self-consistent grain-composition limits.

The TESS young mean duty 0.101 is near the population template upper limit 0.106. This comparison shows that a physically relevant duty scale was omitted from that template. It does not prove acceptance of the material model. The infrared sample has 546 young rapid stars and 78 young hosts after its own quality cuts; our TESS groups have 762 and 114. A valid joint test must match those exact stars and recompute band predictions, covariances, photospheric reference fits and occultation corrections. Corotation radius, stellar flux and type probability can correlate. The appropriate band-weighted correction is a sum of each star's template times its historical probability, not the unweighted mean in our table. At finite excess the ratio to W1 is also nonlinear in the dust flux. No revised infrared significance or albedo confidence interval is claimed.

A useful next test is simultaneous optical and infrared monitoring, with an explicit material-presence or cross-section process. It would condition the thermal prediction on a measured optical state and would remove the unknown historical duty factor. Repeated optical flags alone cannot supply that physical calibration.

## Limits

The models describe threshold flags at sector proxy times. They do not measure material mass. Off can mean no material, a different shape, a shallow dip, or failed detection. Our zero-area off interpretation is a countermodel assumption, not an inferred physical fact. The on-state area distribution can correlate with duty and varies between sectors. We hold it fixed for the sensitivity argument. Parameter uncertainty, inclination and selection effects are not propagated. Stationarity before TESS cannot be tested with these sequences. Without stationarity or another historical supply model, TESS data put no positive lower bound on the cross-section in 2010: one can keep all TESS paths unchanged and choose zero earlier material. Conversely, a persistent unseen reservoir may leave the original infrared prediction appropriate. The infrared non-detection and its reported photometric errors are not challenged by this work.

## Reproduction and rights

Use Python 3.12 with numpy, pandas, scipy, matplotlib and the SCI CLI. From an unpacked publication, run:

```sh
OPENBLAS_NUM_THREADS=1 python files/analyze.py /absolute/path/to/campaign /absolute/path/to/separate_scratch
```

The code verifies all three source ZIPs, checks their manifest IDs, hashes the used members, repeats the conditional calculation and arithmetic checks, and writes results.json, provenance.json and result.png. It also writes derived star records only to the separate scratch. Those records are intentionally excluded from this signed bundle. The stored results and plot are the outputs of this command. The run uses one compute process and one numerical library thread. No new fit or network request is needed once the source ZIPs are available. Source SCI IDs locate exact inputs after campaign relocation.

The package contains original code, text, plot and aggregate model calculations under the exact SCI baseline license. Separate external-data attribution is in files/EXTERNAL_DATA.md. It contains no AllWISE, 2MASS or Gaia record-level extract and no copied source code. Input hashes identify the source versions without relicensing their tables.
