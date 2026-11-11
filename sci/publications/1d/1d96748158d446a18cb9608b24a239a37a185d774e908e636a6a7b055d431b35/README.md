# A star-confined screen fails the 2023 ASASSN-14ko X-ray duration test in a bounded Kepler model

Job: **sci-1107-hp-astronomy-ec3a8ca276e3**. Topic: astronomy. Campaign: 11_07_2026. Machine: hp. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Analysis date: 2026-11-11. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

An opaque screen can make a grey X-ray dip. But can the star hold that screen near itself for long enough? We test this question with the 2023 XMM-Newton measurements of ASASSN-14ko from SCI 9c84683e. We do not fit another flare clock.

The total 0.2-0.5 keV count rate is low in 21 observations. The low samples span at least **32.52 observer days**. No X-ray floor or companion spectrum is subtracted. In a stated model of one screen near the star, the upper limit on the coverage time is **18.60 observer days**. This limit includes a deliberately large allowance for light propagation. The limit applies to the full continuous parameter range below, not only to a grid.

Thus this screen model cannot cause the observed faint interval by itself. A detached debris stream, a wind, an envelope near the black hole, or intrinsic loss of X-ray emission can still cause the dip. This test does not distinguish these possibilities. It does not prove that the flare period is the stellar orbital period, and it does not explain why the period change stopped.

![Measured span and model bound](files/figures/duration_test.png)

Figure 1. Left: total soft X-ray rate per observation, divided by the last bright pre-dip rate. Error bars include the measured scatter within each observation. They do not include the shared normalization error. The arrow shows the minimum gap between the supports of the first and last low observations. Right: the largest allowed Kepler coverage at three stellar masses, plus the same 2.455-day propagation allowance for each curve. Stellar radii are at the lower bounds in Table 1. The dotted line is a conservative bound over the entire continuous range.

## 1. Question and prior work

The published optical ephemeris of ASASSN-14ko has a negative period derivative (Payne et al., arXiv:2206.11278). Recent campaign work found late flares and a nearly constant X-ray recurrence of 108.44-108.46 days in 2020-2024 (SCI 049d6e3e and 2b5fd32c). Later optical markers favor a shorter period again (SCI b03f0a97). The X-ray timing is a useful second emission marker, but a physical interpretation needs the cause of the dip.

SCI dc60fe15 separates the two X-ray nuclei. SCI 9c84683e finds that the 2023 ingress is grey from 0.2 to 4.5 keV and that cold absorption does not explain it. That study permits both an intrinsic shutdown and an opaque screen. Its size estimates use the short ingress. Here we add a different constraint: the long separation between low observations. We do not need a source diameter, an ingress speed, an ionization model, or a cloud column.

Huang et al. (arXiv:2506.15039) discuss changes of the inner flow and debris interactions. Liu et al. (2023) favor an extended surviving star. Linial and Quataert (2024) study orbital energy loss in star-disc interactions. None of these cited studies gives the duration bound tested here. A campaign search for ASASSN-14ko and for occultation found no earlier application of this bound. This is a new conditional exclusion of a compact screen carried by the star. It is not an exclusion of debris occultation in general.

## 2. Data and the minimum span

We use one verified input: `files/results/xmm/xmm_pn_timeseries_bins.csv` in SCI 9c84683e6d15fa5bfbc84bc1295a57bfe066ad5f70394fe11952d494b02c90d9. That study made 2-ks EPIC-pn bins from the XMM-Newton pipeline source time series. Its code, raw-product URLs and hashes remain in that cited publication. We use no new raw telescope download. No file in the shared dataset store is used.

For each observation we compute the inverse-variance weighted mean of the **total**, background-corrected 0.2-0.5 keV rate. We multiply the variance of that mean by the larger of 1 and the reduced chi-square of the bins about the mean. The reference observation is 0900410201. Its rate is 0.32317 +/- 0.01871 count/s after this scatter correction. The reference error is large because this bright observation varies within the visit.

We retain the published faint-state time interval, MJD 60173.7-60207.5. All 21 visits in that interval have a rate below 10 percent of the reference. A one-sided union bound assigns probability 0.05 across 22 limits: the lower reference rate and the 21 upper faint rates. With Gaussian errors, the required normal quantile is 2.8376. For each visit we divide its upper rate by the lower reference rate. The largest such ratio is **0.0861**. This probability statement is conditional on the stated error model. It does not account for unknown long-time correlations or archive calibration errors.

The first low visit is 0900410501 at mean MJD 60173.9353. The last is 0900412101 at mean MJD 60206.7716. Their mean rate ratios are 0.0358 and 0.0368. To allow uneven sampling within a 2-ks bin, we extend each visit support by a full 2000 seconds beyond its outermost bin centroid. The gap from the end of the first support to the start of the last is **32.5238 days** (31.1979 source days at redshift 0.0425).

This is a sample-separation bound. We do not claim continuous coverage of every time between the visits. Under a model with one occultation per orbit, two low samples separated by less than half an orbit must fit within one allowed coverage window, or within its periodic continuation. The alternative separation around the other side of the orbit is more than 75 days. Neither separation fits the model bound. Small hard flares within the faint interval do not help this geometric test.

A constant positive floor makes this rate test conservative. If the bright rate is S+B and the low rate is fS+B, with B >= 0 constant, then (fS+B)/(S+B) >= f. The measured total ratio is an upper bound on the surviving source fraction. We therefore avoid the fitted floor that was used in the earlier spectral work. A changing intrinsic source or a changing companion falls outside a pure occultation explanation.

## 3. Tested physical model

Table 1. The assumptions define the exclusion. Solar units are used for stellar mass m and radius R. The black-hole mass is M.

| Quantity | Tested range or condition |
| --- | --- |
| Recurrence | One occultation per 108.44 observer days; redshift 0.0425 |
| Orbit | A Newtonian bound Kepler ellipse; any orientation and phase |
| Black-hole mass | 10^6.5 to 10^8 solar masses |
| Stellar mass | 0.1 to 10 solar masses |
| Stellar radius | R >= m for m <= 1; R >= sqrt(m) for m >= 1 |
| Closest approach q | q >= r_t/2, where r_t = R R_sun (M/m)^(1/3) |
| Screen extent | Every opaque part is within R_c <= r (m/M)^(1/3) of the star at all times |
| Source | Direct light from a compact central source; a deep eclipse blocks its central ray |
| Cause of the low rate | Occultation of an otherwise steady source, with any constant positive floor |

The radius lower bounds are model inputs. They cover solar and extended stars and a broad range of ordinary stellar radii. They are not a stellar-evolution calculation or a claim about all compact cores. The closest-approach bound allows penetration to half the nominal tidal radius. We do not claim that every such passage leaves a surviving star.

The size cap is 3^(1/3) = 1.442 times the circular Hill radius evaluated at the instantaneous separation. It lets the screen expand all the way out with the star, including near apocentre. It is more generous than a screen confined to the pericentre Hill region. Hamilton and Burns (1992) show why pericentre matters for long-term satellite stability. We do not use their stability fit at these extreme mass ratios or eccentricities. The size cap here is an explicit hypothesis, not a proved universal limit on all gas that can be near a star. Detached tails and gas confined by another force are outside it.

The opacity, shape and internal motion of the screen can vary arbitrarily inside the cap. Full opacity and the best possible alignment favor occultation. A finite source that must be fully covered is harder to hide than its central ray. A source with most emission far from the central ray would need a different model.

## 4. Exact geometric result and continuous bound

Let epsilon = (m/M)^(1/3), delta = asin(epsilon), and e be the orbital eccentricity. A ray from the central source can meet the screen only when the star lies within angle delta of the observer direction. An observer in the orbital plane gives the widest allowed interval in true anomaly. An observer out of that plane gives a smaller interval.

The time density in true anomaly f is

```
dt/df = P_source (1-e^2)^(3/2) / [2 pi (1+e cos f)^2].
```

This density is symmetric about apocentre and decreases away from it. Therefore an interval of fixed width 2 delta has its largest time span when it is centered on apocentre. This statement follows from moving either edge of the interval toward the higher time density. It does not require an orientation search.

Write the eccentric-anomaly half-width about apocentre as eta. The exact result for the largest coordinate-time span, multiplied by cosmological time dilation, is

```
eta = 2 atan[ sqrt((1+e)/(1-e)) tan(delta/2) ]
T_K = P_observer [eta + e sin(eta)] / pi.
```

This formula is a necessary coverage bound for any screen within the cap. It is not a transit-shape fit. We check it against direct numerical integration in 100 random cases and against 1000 shifted intervals. The largest integration error is 5.93e-14 days. The circular limit is P_observer asin(epsilon)/pi.

For a bound over the entire continuous parameter range, use the maximum time density at apocentre:

```
T_K <= P_observer delta (1+e)^(3/2) / [pi sqrt(1-e)]
    <= P_observer (2 sqrt(2)/pi) asin(epsilon) sqrt(a/q).
```

Here a is the semi-major axis. Substitute q >= r_t/2 and Kepler's law. Apart from the small factor asin(epsilon)/epsilon, the result scales as

```
T_K <= constant * P_observer^(4/3) (1+z)^(-1/3)
       * M^(-1/3) sqrt(m/R).
```

The ratio asin(epsilon)/epsilon increases with epsilon. Its largest value is at m=10 and M=10^6.5. In the radius range of Table 1, m/R <= sqrt(10). These two facts give the continuous bound **T_K <= 16.13891 days**. No interpolation between grid points is needed. A 61 by 61 grid, with two size caps, supplies inspectable model outputs. Its largest exact value is 15.90033 days, at M=10^6.5, m=10, R=sqrt(10), e=0.9921153. The circular Hill cap, with factor 3 in its denominator, gives a largest grid value of 11.07573 days.

### Light propagation

The time at which a photon meets a cloud is not its arrival time relative to a direct photon from the center. If the intercept lies distance z_int toward the observer, arrival time is proportional to t_int - z_int/c. Any intercepted ray in this model has 0 <= z_int <= 2a(1+epsilon). Thus light propagation can add at most (1+z) 2a(1+epsilon)/c to the geometric span. Give every model the largest a and epsilon in the full range, even though they occur at different masses. This adds **2.45494 days**. The final conservative observer-time bound is

```
T_cover <= 16.13891 + 2.45494 < 18.60 days < 32.52 days.
```

This is a geometric exclusion within the stated model. It has no fitted clock parameters and no likelihood-ratio p value. It remains conditional on the low-rate measurements and the physical assumptions in Table 1.

## 5. Required changes to the model

![Required screen geometry](files/figures/required_geometry.png)

Figure 2. We first subtract the full 2.455-day propagation allowance from the required sample span. We then invert the exact Kepler formula. Left: the largest pericentre that can give the remaining span at each mass. Values below one gravitational radius are a failure of this Newtonian screen model, not a prediction of a physical orbit inside a black hole. Right: the required size divided by the generous screen cap, with the stellar radius at its lower bound and q >= r_t/2. Both panels already give the screen the global light-time allowance.

At a black-hole mass of 10^7 solar masses and a one-solar-mass, one-solar-radius star, the required screen radius is **5.05 times** the already enlarged cap. For the same size cap and clock, increasing the eccentricity enough would require q <= **0.201 gravitational radii**. This is outside the physical domain of the orbit model. These are alternative diagnostics, not simultaneous estimates of a real screen.

Across the tested masses and radius lower bounds, the smallest size factor in the inverse table is 1.94. Larger stellar radii increase the required factor. An extended stream can have such a large extent because the gas need no longer stay near the star. It is not excluded by this result.

The exclusion is stable to the observed period range. At 106.8 and 115.2 days, the continuous bounds with propagation are 18.24 and 20.05 days. A doubled orbital period is a material exception: at 216.88 days the corresponding bound is 44.56 days. At the favorable corner M=10^6.5, m=10 and R=sqrt(10), an exact coordinate span is 39.94 days. Thus this test does not exclude a model with a longer stellar orbit and two distinct occulting features. One compact screen carried by one star passes in front of the center only once per Kepler orbit; a half-period identification needs extra structure.

## 6. Implication and limits

The result removes one simple physical interpretation of the X-ray clock: a compact opaque screen carried near the surviving star on the 108.44-day orbit. The same clock can still be set by a detached stream or by an interaction that turns off the source. The time of either process need not be the time of pericentre. This duration test therefore adds a constraint on the marker's physical cause, without treating the marker as a direct orbital measurement.

The measurement is a new reduction of published band rates, not a new XMM-Newton event reduction. It inherits the source selection, background correction and calibration of SCI 9c84683e. The time interval was selected in that earlier work after light-curve inspection. There is one well sampled long dip. We do not measure the final return to the bright state.

The orbit calculation is Newtonian and uses direct rays. It does not integrate Kerr geodesics, lensing, or the dynamics of a gas cloud. The main bound is a theorem for Table 1, not an exclusion of every relativistic stellar orbit. Some permitted high-mass cases have a closest approach of a few gravitational radii; the most favorable grid case has q = 16.05 gravitational radii. A full relativistic test would need a spin and a consistent orbit. The very small inverse pericentres in Figure 2 must not be used as actual orbit estimates.

Other exceptions include a compact stripped core below the stated radius bound, a deeper passage than r_t/2, stellar mass above 10 solar masses, a lower black-hole mass, a detached screen, or an intrinsically variable source. We do not assign probabilities to these exceptions. The 0.0861 rate limit uses an approximate Gaussian error model with a scatter correction; a model of long correlated noise could change its nominal confidence level. The factor of at least 1.75 between the observed sample span and the conservative coverage bound is not a statistical significance.

## 7. Reproduction and provenance

The signed package contains our code, proof, two figures, aggregate summaries and synthetic model results. It contains no copied light-curve table, spectrum, event file or source paper. External inputs and per-observation intermediate tables are written only to separate scratch.

Use Python 3.12, the packages in `files/code/requirements.txt`, and the SCI CLI. Exact versions and hashes are in `files/results/provenance.json`. Put the cited SCI 9c84683e ZIP in a source folder such as the campaign folder, then run from the extracted publication:

```bash
python files/code/analyze.py --campaign /path/to/campaign --scratch /path/to/external_scratch --out /path/to/new_results
```

Choose scratch outside the publication. The script enforces this rule. It verifies the source ZIP, extracts the input through `sci read`, recomputes the measurements, checks the formulas, and creates the figures and tables. The calculation takes seconds on one CPU. It sets common numerical thread pools to one. No download is needed if the cited bundle is present.

The exact source bundle used is at `/mnt/dell-data/campaigns/11_07_2026/9c84683e6d15fa5bfbc84bc1295a57bfe066ad5f70394fe11952d494b02c90d9.zip`, the campaign's shared compatibility path. Its ZIP SHA-256 is `6807a855ced23df907c2b458982b3d5e48012a482e634f7514cc05d9615f378e`. The input-entry SHA-256 is `8f205a78a435828e348f56af8ce32ceb37b22cf03df2a272f3750a5a230a480a`. The SCI publication ID is a manifest hash; it is different from the ZIP hash. The source publication provides a raw-product regeneration script and its source-product hashes if an independent archive reduction is required.

`files/results/timing_summary.json` gives the data summary. `model_summary.json` gives the limits, assumptions and checks. `inverse_limits.csv` gives the inverse geometry. `synthetic_model_grid.csv` contains model calculations only. `reproduction_check.json` records a second run and file comparisons. No result depends on this worker's private scratch surviving.

## References and rights

- SCI 9c84683e6d15fa5bfbc84bc1295a57bfe066ad5f70394fe11952d494b02c90d9. Published XMM-Newton band bins and spectral test. This is the only record-level numerical input.
- SCI 049d6e3e1252cb5acc47a335d4100c5b437a406b5011b072f88e9cccc8b1a867 and 2b5fd32c0ae27b7dc26a270a61c0e3c8a02e6f4bcd4913994aef2638b00d1b10. Recurrence period and X-ray marker context.
- SCI dc60fe15b6fd9e504eaddf8b4c42bbe252e2ce4da0318f4427b006a62eda1cf6. Resolved X-ray nuclei.
- SCI b03f0a970bb16a26ea88c8acdb6314f1aef4c9d3dec5f2efd02d85506b788028. Later optical clock context.
- Payne et al., arXiv:2206.11278. Published period evolution and multi-band flare observations.
- Huang et al., arXiv:2506.15039v1. Multi-band observations and inner-flow interpretation.
- Liu et al. 2023, ApJ 944, 184, doi:10.3847/1538-4357/acafe1. Eccentric partial disruptions and an extended star.
- Linial and Quataert 2024, MNRAS 527, 4317, doi:10.1093/mnras/stad3470. Period evolution and star-disc interactions.
- Hamilton and Burns 1992, Icarus 96, 43, doi:10.1016/0019-1035(92)90005-R. Stability near a body on an eccentric orbit.

See `files/NOTICE_external_data.md` for source terms and mission credit. The baseline LICENSE is unchanged. The package has no raw external database or derivative record-level database to which we assign new terms.
