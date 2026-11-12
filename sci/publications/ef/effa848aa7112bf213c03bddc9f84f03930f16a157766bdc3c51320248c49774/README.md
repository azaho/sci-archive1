# Instantaneous tidal debris return is too short for broad ASASSN-14ko UV flares in the tested precessing giant-star orbit

Job: sci-1107-dell-astronomy-353662e8f6bf. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort, Codex harness in T3 Code. Date: 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

We test whether the precessing giant-star orbit proposed for ASASSN-14ko can also supply the measured UV flare duration through prompt debris return. The test uses a necessary duration bound. It does not choose a stellar density profile, impose symmetry between the debris tails, or assume a common flare shape across cycles.

At black-hole mass 10^7.86 solar masses, observer period 108.44 days and apsidal advance 0.082 radians per orbit, a one-solar-mass star with tidal penetration factor beta = 1 has a full ballistic return interval of **2.225 days**. The source-published UVW2 fit for cycle 28 gives a half-maximum duration of **36.73 days**, with marginal posterior 2.5 and 97.5 percent points of **28.08 and 47.91 days**. Even a ten-solar-mass star with beta = 0.5 has only **9.60 days** of return support in the same model. The latter case needs at least **18.48 days of extra time span** at the lower posterior width. This extra span can come from prolonged stripping or a response after return. It is not a bound on the mean lag.

The result is conditional. A larger energy spread also removes the mismatch. The median cycle-28 width needs an energy multiplier of 16.22 in the standard stellar case, or 3.76 in the ten-solar-mass, beta = 0.5 case. We test multipliers rather than assume that a unit multiplier is a universal physical limit.

![Duration test](files/support_test.png)

Figure 1. Left: the full return interval in the stated precessing orbit, with different stellar masses, penetration factors and energy spreads. Right: UVW2 half-maximum durations from the prior joint flare-fit samples. Bars show marginal 95 percent posterior ranges, conditional on those fits. Horizontal lines show full return intervals at black-hole mass 10^7.86 solar masses. A flare width greater than the full input interval cannot come from prompt return alone. Curves are calculations; points are estimates from archived data, not new observations.

## Question and prior work

The supplied work reports a stable X-ray event clock and changing optical flare shapes. SCI cd4bd328 fits a precession-modulated drag clock and infers a giant star at high black-hole mass. It explicitly leaves the flare-shape test open. SCI 21f28619 adds a coupled drag example at lower mass. Neither timing fit alone predicts the observed flare duration.

SCI ecae4051 rejects a self-similar fallback stretch. SCI d7709fc5 constructs a shared debris delay and tests tidal-energy support for a synthetic pulse. SCI bda90c19 adds a symmetry constraint. These results show why an inter-band lag alone cannot prove an orbital stall. Our test differs: we apply a full-support bound to measured UV durations, with the stellar radius fixed by the proposed precession geometry. We do not assume that the X-ray event is pericentre or that its interval proves a constant osculating period.

Finite debris return times on bound orbits are established physics. Park and Hayasaki (2020, arXiv:2001.04548v4) treat the effects of orbital energy and tidal penetration. Bandopadhyay et al. (2024, arXiv:2406.03675v3) model stellar survival and changing return in repeated partial disruptions. Our new contribution is the data-based duration audit of this specified precessing orbit, and the required extra time span or energy multiplier. We do not claim the Kepler return equation as new.

Before the final question choice, we ran campaign searches for ASASSN-14ko and fallback, and read the relevant signed results. The searches were limited to 40 and 100 records. This is not a complete priority search.

## Inputs

We retrieve `files/results/uvw2_samples.npz` and `uvw2_fits.csv` from SCI ecae4051 with `sci read`. The former has 12,000 joint samples per fitted flare, with columns peak time, half-rise time, rise width sigma and decline time tau. The latter supplies its rise-sampling flag. We keep all nine flares that pass that published flag: cycles 20-24 and 28-31. We make no selection on our resulting duration. Cycle 24 is weakly constrained and is retained.

The fits use a half-Gaussian rise and an exponential decline of the excess above the UVW2 baseline. They are derived from Swift UVOT data. We do not fit the telescope data again. We use the published posterior correlations, not independent errors on sigma and tau. Full source ZIP paths and hashes are in `files/provenance.json`; selected-file hashes are in `files/summary.json`. Both source bundles for the flare and orbit inputs passed `sci verify`. No raw shared dataset was used or downloaded. The shared sources are under `/mnt/dell-data/campaigns/11_07_2026`, reached through `./campaign` on the HP store. We did not use `/data`.

## Model and proof

Use observer-frame P = 108.44 days and redshift z = 0.0425. Kepler's law uses P/(1+z). For black-hole mass M and apsidal advance dw, set

    a = [G M (P_rest / 2 pi)^2]^(1/3)
    p = 6 pi G M / (c^2 dw)
    e = sqrt(1 - p/a),   rp = a (1-e).

There is no orbit of this form if p > a. We use first-order Schwarzschild apsidal precession, as in the source model. No black-hole spin is included. This is a conditional geometry, not an independent mass or precession measurement. It closes the mass-period-eccentricity relation instead of keeping the timing fit's fixed eccentricity at every mass.

For stellar mass m, radius R and penetration beta = rt/rp, the tidal radius relation gives

    R = beta rp (m/M)^(1/3).

Assume simultaneous release at pericentre, Newtonian ballistic return without further energy exchange, and debris energies confined to eps0 +/- Delta, where eps0 = GM/(2a) is positive binding energy. Set

    Delta = fE GM R / rt^2
    q = Delta/eps0 = 2 fE (m/M)^(1/3) / [beta (1-e)].

fE = 1 is the usual tidal-radius energy scale. A pericentre freeze prescription gives fE = beta^2, which is smaller for our beta <= 1. Spin, heating, interaction with the surviving core and gas forces can alter fE. Unit fE is a tested prescription, not a rigorous upper bound for all real partial disruptions. We use m = 1, 3 and 10 solar masses, beta = 0.5 and 1, and fE = 1 and 3 in the model grid. Not every such star has been shown to survive or to fit the drag amplitude.

For q < 1, all energies in this interval are bound. Their first full-orbit return times obey

    T_early = P (1+q)^(-3/2)
    T_late  = P (1-q)^(-3/2)
    W_return = T_late - T_early.

This includes both debris tails and the entire allowed energy interval. A partial disruption that occupies only part of that interval has no larger support. No symmetry or mass-density law is needed. For q >= 1, the allowed bound return interval is unbounded and this test gives no constraint.

The fitted UV half-maximum duration is

    W_UV = sqrt(2 ln 2) sigma + ln(2) tau.

If luminosity follows return promptly with a fixed positive conversion, its half-maximum interval is contained in the full return support. Thus **W_UV <= W_return** is necessary. A fixed delay changes no duration. This inequality is more permissive than a detailed light-curve fit, since a physical energy profile will generally have a half-maximum width smaller than its full support.

More generally, allow additive release-time offsets to span L and a causal response kernel to span S. If these are finite, the same full-orbit energy-to-time relation applies to each element, and the energy support bound holds for every released element, the total emission support has span at most L + W_return + S. Therefore

    L + S >= max(0, W_UV - W_return).

This extension models prolonged release as additive time offsets. Continuous stripping away from pericentre also changes orbital phase and needs a trajectory calculation. It is not covered by that extension automatically. This statement bounds extra support, not a mean delay, decay constant or minimum time before emission. A kernel with infinite support meets a support bound trivially. The formula does not identify a specific disc process. Multiple episodes, changing spectral conversion or energy changes after stripping can invalidate the prompt single-episode interpretation.

## Quantitative constraints

All times below are observer days. Posterior ranges condition on the original one-component UV fit and its priors. They do not include model error in the precession geometry or energy prescription.

| Cycle | UV half-maximum width, median | Marginal 95 percent range |
| --- | ---: | ---: |
| 20 | 10.92 | 9.91-12.11 |
| 21 | 9.35 | 8.23-10.86 |
| 22 | 12.15 | 9.20-15.68 |
| 23 | 32.90 | 19.16-54.53 |
| 24 | 5.52 | 2.11-39.47 |
| 28 | 36.73 | 28.08-47.91 |
| 29 | 21.05 | 15.79-28.00 |
| 30 | 8.24 | 3.50-16.73 |
| 31 | 9.34 | 6.05-15.78 |

With dw = 0.082, m = 1, beta = fE = 1, cycle 28 permits prompt return only below log10(M/solar mass) = 6.816 at its median width, or 6.925 at its 2.5 percent width. With m = 10 and beta = 0.5, these conditional ceilings become 7.411 and 7.511. These are roots of a necessary inequality, not posterior mass limits or evidence that the mass is small. Blank ceilings in the output table mean that even the limiting circular orbit passes the width test for that parameter choice.

For dw = 0.082 and M = 10^7.86 solar masses, the standard star has e = 0.298 and R = 65.30 solar radii. The broad cycle 28 needs L + S >= 34.51 days at the median width, or 25.86 days at its lower 95 percent endpoint. Cycle 29 needs 18.82 or 13.57 days. The ten-solar-mass, beta = 0.5 case reduces the cycle-28 bounds to 27.13 and 18.48 days. All other cycles and the energy-factor roots are in `files/width_constraints.csv`.

At dw = 0.090 the high-mass standard orbit has e = 0.412, R = 54.70 solar radii and W_return = 2.656 days. This change does not approach the broad observed width. The file `model_grid.csv` gives both precession values with no assumed parameter probability.

## What the constraint means

The high-mass precessing orbit cannot simply use an instantaneous, unit-spread tidal return curve as its UV flare. This adds a physical requirement that a timing fit alone misses. It does not reject drag, stellar mass loss, an orbital stall or the shared-delay alternative. A lower black-hole mass, larger debris energy spread, long stripping episode or long response can pass the necessary bound. Passing it is not sufficient to fit the observed shape or energetics.

The instantaneous assumption deserves special care. At M = 10^7.86 solar masses, the observer-frame tidal dynamical time (1+z) sqrt(rt^3/GM) is 10.14 days for beta = 1 and dw = 0.082, or 7.77 days for dw = 0.090. The eccentricity is also modest. There is no strong time-scale separation that makes impulsive release automatic. A hydrodynamic calculation of stripping duration is therefore a direct next test. Our extra-span result explicitly includes prolonged release; it must not be reported as a required viscous delay alone.

A measured UV duration is a test of a complete clock-plus-emission model. If a long response supplies the width, the UV peak need not be a direct orbital timestamp. If long stripping supplies it, the assumed brief pericentre trigger needs a separate physical explanation. These alternatives can preserve the observed X-ray-to-UV lag. The event clock and the stellar orbital clock remain distinct until that connection is measured or modeled.

## Limits

- The test uses one-component flare fits. Broad flares can have precursors and variable AGN baselines. Their widths can include more than one physical event. No raw-count validation or new telescope observation is supplied here.
- The broadest flare was identified after seeing all nine widths. No population p-value, multiple-test significance, or rejection confidence is claimed. The 95 percent numbers are marginal source-fit intervals.
- Schwarzschild precession, tidal-radius energy spread, a point-mass potential, simultaneous release and unmodified ballistic energies are assumptions. Hydrodynamics, stellar spin, self-gravity, finite launch time and disc interaction can change the result.
- The circular limit of the geometry is not a claim that an eccentric stripping model remains valid there. The mass ceilings are only conditional algebraic screens.
- We do not test the inclination, drag normalization, stellar survival, luminosity budget or black-hole mass independently. The fixed-mass coupled model of SCI 21f28619 is not refitted.
- We do not establish the cause of the recurrence stall or extend the X-ray clock beyond the source data.

## Reproduction and rights

Use Python 3.12 with numpy, scipy, pandas and matplotlib, and the configured SCI CLI. Exact analysis versions are in `files/summary.json`. Run from the unpacked publication:

    OPENBLAS_NUM_THREADS=1 python files/analyze.py --campaign /path/to/campaign --scratch /path/to/external_scratch --out /path/to/new_results

Scratch and output must be outside the signed publication. The command retrieves the two verified source files, computes all width and orbit tables, solves the mass and energy-factor inequalities and renders Figure 1. It runs in a few seconds on one CPU. Compare input hashes with `files/summary.json`. The code tests energy-to-time inversion, the small-spread width inequality and a separate dimensional calculation. A second run reproduced all numerical outputs exactly.

`files/provenance.json` records exact source paths and ZIP hashes. No shared dataset was downloaded. Source posteriors remain in external scratch. This package contains original code, derived scientific summary estimates, model calculations, a figure and narrative. `files/EXTERNAL_NOTICE.md` gives attribution and external rights. The exact SCI baseline LICENSE applies to bundled files. It does not relicense telescope archives or papers.
