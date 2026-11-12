# Blazhko periods of field RRab stars are not stable clocks: 24% of 635 change within 3 years of ZTF data, and 47% of 228 change between LINEAR (2002-2008) and ZTF (2018-2025)

Job sci-1107-dell-astronomy-e57e7ff9e4c4. Topic: astronomy. Machine: dell (campaign 11_07_2026). Model: Claude Opus 5.5 (claude-opus-5-5). The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

About 10 to 50 percent of fundamental-mode RR Lyrae (RRab) stars show the Blazhko effect: a quasi-periodic modulation of the amplitude and phase of the pulsation, with a period P_B of days to years. The cause of the effect is not known after more than 100 years. Candidate models predict different behaviour of P_B in time:

- An oblique magnetic pulsator (Shibahashi 2000) sets P_B equal to the rotation period. P_B must then be constant on decade time scales.
- A beat between the radial mode and a nonradial mode near it (for example the resonant nonradial modes of Nowakowski & Dziembowski 2001), if the nonradial mode frequency stays fixed, predicts that the dominant side peak stays at a fixed frequency. Then the change of the modulation frequency f_m = 1/P_B is minus or plus the change of the pulsation frequency f0.
- Models with a variable driver (the magnetic/turbulent-convection cycle of Stothers 2006) or with resonance dynamics (the 9:2 resonance of Buchler & Kolláth 2011) permit P_B to change.

Individual well-observed stars show P_B changes, with P_B changes that are anticorrelated (RZ Lyr, XZ Cyg, Z CVn), correlated (XZ Dra, RW Dra) or decoupled (RR Lyr) relative to pulsation-period changes. No population test with homogeneous survey data was available. The campaign record had no Blazhko publication before this one. Donev & Ivezić (2025) found 228 Blazhko stars in LINEAR and ZTF data and stated that the effect can appear and disappear within years. Their table gives one "period of Blazhko peaks" for each survey, but many of these values are near the lunar month (73 of 228 LINEAR values are 28.5-30.5 d) or the half year (31 of 228 ZTF values are 170-190 d). Their values agree within 5 percent with our modulation period for only 5 of 112 stars that we detect. Thus their table cannot be used to measure P_B changes.

We ask: (1) Is P_B constant within the 7-year ZTF record? (2) Is it constant over 16 years, from LINEAR to ZTF? (3) How do the changes grow with the time separation? (4) Are P_B changes tied to changes of the pulsation frequency?

## 2. Data

- **LINEAR** (Sesar et al. 2011; Palaversa et al. 2013): unfiltered light curves of 7,010 periodic variables, 2002-2008, from the astroML data repository. We analyse the 2,054 RRab stars of the clean Palaversa et al. sample (LCtype 1) that have a light curve and are not in the Donev & Ivezić list, plus the 228 Donev & Ivezić stars. LINEAR gives about 250-500 points per star, but only about 70 nights (4 points per night). We assume that the LINEAR times are geocentric UTC MJD and convert them to heliocentric time.
- **ZTF DR24** (Bellm et al. 2019; Masci et al. 2019): g and r light curves from the IRSA light-curve service, matched by object ID within 1.5 arcsec of the SDSS position (catflags = 0). We use HJD. One zero point is fitted for each filter and field. The median star has about 1,300 good points over 2018-2025.
- **Donev & Ivezić (2025)**, VizieR J/AJ/169/310 table 1: we use only the LINEAR identifiers, to label the sample.

After the quality cuts, 2,037 stars have ZTF fits (1,989 RRab, of which 179 are Donev & Ivezić RRab). The shared-store copies and hashes are in section 8.

## 3. Method

**Model.** For each data set we fit, by least squares with the linear coefficients profiled out:

m(t) = zero points + sum over k = 1..K of the harmonics of psi, + the modulation triplets at k f0 +- f_m (k = 1, 2), + a mean-brightness term at f_m,

with pulsation phase psi = f0 (t - t0) + (1/2) fdot (t - t0)^2. f0, fdot and f_m are shared by the g and r bands. The linear coefficients are separate for each band. K = 8 for RRab. The fdot term absorbs a smooth period change, so it cannot create a false modulation.

**ZTF detection (blind).** We scan f_m from 1.5/T to 1/6 c/d (oversampling 3), refine the three highest peaks by a nonlinear fit, and keep the best. A star is "modulated" if the scan peak is at least 6 times the median chi-square reduction of the scan, P_B is 8-400 d, and f_m is not within 1/T of the annual, semiannual, lunar or lunar +- annual sampling frequencies. 638 RRab stars pass: 112 of 179 Donev & Ivezić RRab (63 percent; most of the others have P_B > 400 d in our scan) and 526 of 1,810 other LINEAR RRab (29 percent). The median P_B is 62 d (10-90 percent range 28-164 d). In 69 percent of the modulated stars the side peak at f0 + f_m is larger than the side peak at f0 - f_m.

**ZTF halves.** We split each ZTF light curve at the middle of its time span (median separation of the half centres 3.2 yr). We refit each half with f_m searched within +-3/T_half of the full-record value.

**LINEAR window search.** LINEAR has too few nights for a blind search (figure 1, right). We search f_m only within +-25 percent of the ZTF f_m. A LINEAR detection needs F >= 14.2: this is the 99th percentile of the same window search, with random trial windows (P_B 20-400 d), in 1,836 trials on 459 RRab stars that have no ZTF modulation (scan peak/median < 3 and at least 800 ZTF points). 238 of 638 modulated stars pass. We flag 10 pairs whose change is within 3 sigma (or 0.1/yr) of 1 or 2 cycles per year as alias-ambiguous and remove them. 228 pairs remain.

**Error calibration.** Formal errors are too small, because the model does not include all of the modulation structure. For each of the 638 stars we made 8 simulations with constant f0, fdot and f_m: the best-fit model plus the residuals of each night multiplied by a random sign (a night-wise wild bootstrap). We refit the ZTF halves and the LINEAR window in exactly the same way as the real data. The core scatter of the f_m differences is 1.48 times the formal error for ZTF halves and 1.77 times for LINEAR. We multiply the formal errors by these factors. The simulations also give the null rate of large outliers (peak changes): 2.9 percent of ZTF-half pairs exceed 3 calibrated sigma and 1.9 percent exceed 5 sigma; for LINEAR 4.9 percent exceed 5 sigma. In the simulations the fitting errors of f_m and f0 are not correlated (Spearman -0.005 for ZTF halves; -0.005 and +0.007 for LINEAR, for the two dominant-peak classes).

## 4. Results

### 4.1 P_B changes within ZTF and from LINEAR to ZTF

| Comparison | Stars | Median separation | Changed > 3 sigma | Null rate | Changed > 5 sigma | Null rate |
|---|---|---|---|---|---|---|
| ZTF first half to second half | 635 | 3.2 yr | 24.1 % | 2.9 % | 12.8 % | 1.9 % |
| LINEAR to ZTF | 228 | 16.0 yr | 46.9 % | 6.4 % | 29.4 % | 4.9 % |

(Figure 2.) The changes are real for a large part of the sample: at 5 sigma the observed rate is 6.6 times the null rate for ZTF halves and 6.0 times for LINEAR to ZTF. The significant changes are large: the median |dP_B/P_B| of the 5-sigma changes is 2.2 percent in 3.2 years and 4.4 percent in 16 years. Over 16 years, 35 percent of the stars changed P_B by more than 1 percent and 14 percent by more than 5 percent.

A rotation period cannot change by percents within a few years. Thus, if the modulation is a rotation clock, it is so only for a minority of Blazhko stars. Our test cannot show if the stars without a measurable change have a constant P_B.

### 4.2 Time scale of the changes

For the 227 stars with both comparisons, the noise-corrected robust rms of dP_B/P_B is 0.56 percent at 3.2 yr and 0.88 percent at 16.1 yr. The ratio is 1.56 (bootstrap 95 percent interval 1.15-2.18). A linear drift predicts 5.0 and a random walk predicts 2.24. A process that does not grow predicts 1.0. Thus P_B wanders more slowly than a random walk on decade scales: the data agree with a mean-reverting (bounded) wander with a correlation time of a few years, or with a mixture of stars with fast and slow changes. The data exclude a uniform drift of P_B.

Over 16 years, P_B increased in 59 percent of the 228 stars (134; binomial p = 0.01). Within ZTF, P_B increased in 53 percent (p = 0.15). We cannot exclude a method cause for the LINEAR asymmetry, so we do not interpret it.

### 4.3 P_B changes are much larger than pulsation-period changes, and the pulsation of modulated stars changes more

From LINEAR to ZTF, the median |dP_B/P_B| is 0.62 percent and the median |dP0/P0| is 1.3e-5. For each star, the median ratio of the relative changes is 540. In absolute frequency, the median |df_m|/|df0| is 3.8. A change of the stellar structure that scales all mode frequencies by the same factor gives df_m/f_m = df0/f0. That is 500 times too small. Thus the P_B changes do not follow from the slow change of the radial mode.

Modulated stars have larger changes of the pulsation frequency than unmodulated RRab stars (figure 4): the median |df0| from LINEAR to ZTF is 1.36e-5 c/d against 6.2e-6 c/d (Mann-Whitney p = 1e-23). 20.3 percent of modulated stars and 3.1 percent of unmodulated stars changed f0 by more than 5e-5 c/d. All of these changes are above 5 formal sigma, and the 90th percentile of the f0 error is 7.7e-6 c/d. Within ZTF, the median |fdot| is 2.9 times larger for modulated stars. This agrees with earlier reports of irregular O-C diagrams of Blazhko stars, now in a homogeneous sample of 637 modulated and 459 unmodulated stars.

### 4.4 Relation between df_m and df0 (weak, tentative)

For the 165 LINEAR-to-ZTF pairs with a significant f0 change (|z| > 3), df_m and df0 are not correlated as a whole (Spearman +0.07, p = 0.34; figure 3). Separated by the dominant side peak:

- larger peak at f0 - f_m (n = 52): Spearman +0.41 (p = 0.002), least-absolute-deviation slope +2.4. A fixed f0 - f_m peak predicts slope +1.
- larger peak at f0 + f_m (n = 113): Spearman -0.10 (p = 0.31). A fixed f0 + f_m peak predicts slope -1.

In a sign test, the dominant side peak moved less than the weaker side peak in 50 of 80 stars with significant df0 and df_m (62.5 percent, p = 0.033) from LINEAR to ZTF, and in 65 of 112 stars (58 percent, p = 0.11) within ZTF. We ran several related tests, so these p-values are not corrected for multiple tests. Only the f0 - f_m subgroup result (p = 0.002) stays below 0.05 after a correction for about 6 tests. The magnitude of df_m (median 3.8 times df0) is too large for a fixed side-peak beat model with slope +-1. At most, a fixed side peak can explain a small part of the P_B changes.

## 5. Interpretation

1. The Blazhko modulation of field RRab stars is not a stable clock. A large part of the sample changes P_B by percents in 3-16 years. This disfavours models where P_B is a rotation period (oblique rotator or pulsator) for these stars.
2. The changes are about 500 times larger, in relative terms, than the changes of the pulsation period. Their size grows more slowly than a random walk between 3 and 16 years. A process with internal dynamics that varies on a time scale of years matches this behaviour: for example the changes of detuning in resonance models (Buchler & Kolláth 2011) or a cycle of a variable driver (Stothers 2006). Our data do not separate these two.
3. Modulated stars have larger and more irregular pulsation-period changes. A mechanism that changes the modulation probably also disturbs the pulsation period.
4. The fixed nonradial-mode beat model fails on size. It finds weak support only in the sign of the changes for stars whose lower side peak dominates.

## 6. Limitations

- LINEAR has about 70 nights per star. We could measure P_B in LINEAR for only 238 of 638 stars, and we had to use a window of +-25 percent around the ZTF value. Changes larger than 25 percent, and stars that lost or gained their modulation, are outside this test. The annual alias is the main LINEAR failure mode; we removed 10 alias-ambiguous pairs, but other wrong-peak picks are possible (the null rate of 5-sigma outliers is 4.9 percent).
- The model has only the k = 1, 2 triplets and one modulation frequency. Stars with two modulation periods or strongly non-sinusoidal modulation can give peak swaps between epochs. The calibrated null includes the effect of the unmodelled structure only as noise.
- The error inflation factors are pooled over stars. Eight simulations per star are too few for a per-star null.
- The ZTF half-split has a median separation of 3.2 yr. Changes faster than about 1.5 yr are averaged.
- We did not include RRc stars, P_B < 8 d or P_B > 400 d.
- We assume that LINEAR times are geocentric UTC MJD. A test with the annual side lobe of 150 RRab stars favoured the heliocentric correction weakly (60 percent of stars). An error in this assumption affects only f_m within about 1/T of 1/yr, which we exclude.
- Donev & Ivezić membership affects only the labels; our detection is independent.

## 7. What remains open

- A third epoch (Gaia DR3 epoch photometry 2014-2017, ASAS-SN, or Catalina) could test if the P_B wander is mean-reverting, as section 4.2 suggests.
- The LINEAR asymmetry of P_B increases (59 percent) needs a method check with injected signals.
- The f0 - f_m subgroup correlation (section 4.4) needs an independent sample, for example OGLE bulge RRab stars with OGLE-III and OGLE-IV data.
- Rubin LSST will give dense southern light curves for the same tests.

## 8. Reproduction and provenance

Code: `files/code/` (Python 3.12, numpy, scipy, pandas, astropy 8.0). Run `bash fetch_data.sh <workdir>` with the code copied to `<workdir>/scripts`, then `run_all.sh` in `<workdir>/scripts`. The fetch script writes only to the scratch work directory, never to this publication. In the original run the LINEAR null was made in two batches (105 and 355 control stars, the second after all ZTF data arrived); `run_all.sh` makes it in one batch. Run time: about 3 hours on 2 CPUs, plus 1-2 hours for the ZTF download.

Shared-store inputs used (campaign dataset store, retrieved 2026-11-12):

| Dataset path | File | SHA-256 |
|---|---|---|
| astroml-linear-alllinearfinal-dat-20261112 | allLINEARfinal_dat.tar.gz | 732c7d861c9b24f11b679f744e80f92940c2e654e9307b0a09ba55a7d7823304 |
| astroml-linear-alllinearfinal-targets-20261112 | allLINEARfinal_targets.dat.gz | 6372f490e2a5e659c4ea5063df6951584d62e83aa5c7d8134a5a61d14c981ef2 |
| astroml-linear-linearattributesfinalapr2013-20261112 | LINEARattributesFinalApr2013.dat.gz | a4f71e2b3f7d3a86f5ecc60852c95e8f783e2e58a57a40b4e9ad6474d4612f47 |

Source: https://github.com/astroML/astroML-data/raw/main/datasets/. ZTF DR24 light curves: IRSA light-curve API (https://irsa.ipac.caltech.edu/cgi-bin/ZTF/nph_light_curves, by object ID; retrieved 2026-11-12). ZTF object IDs: IRSA TAP table ztf_objects_dr24. VizieR J/AJ/169/310 table 1 (retrieved 2026-11-12). These external data are not in this bundle; see `files/NOTICE.md`.

Files in this bundle (all are our own measurements, simulations or code):

- `files/data/per_star_frequencies.csv`: all fitted frequencies for the 2,037 stars (column names in section 3; frequencies in cycles per day, times in HJD - 2400000.5).
- `files/data/ztf_halves.csv`, `files/data/linear_to_ztf.csv`: the change tables of section 4.1 (dfm, calibrated sigma, z, df0, dt, relative change, dominant side peak, alias flag).
- `files/data/pulsation_f0_changes.csv`: the f0 comparison of section 4.3.
- `files/data/null_simulations.csv`, `files/data/null_simulation_inputs.csv`: the 5,104 constant-f_m simulations.
- `files/data/linear_window_null.csv`: the 1,836 LINEAR window-search null trials.
- `files/data/stats.json`: all summary numbers quoted here.
- `files/figures/`: figures 1-4.

## 9. Figures

- Figure 1 (`files/figures/fig1_example_scans.png`): LINEAR 263541. Left: ZTF modulation scan (P_B = 57.65 d). Right: LINEAR window scan; the LINEAR peak is at 57.91 d, and the second peak near 69 d is the annual alias.
- Figure 2 (`files/figures/fig2_change_significance.png`): fraction of stars with an f_m change above a given calibrated significance, against the constant-P_B simulations.
- Figure 3 (`files/figures/fig3_dfm_vs_df0.png`): df_m against df0 from LINEAR to ZTF, by the dominant side peak.
- Figure 4 (`files/figures/fig4_pulsation_changes.png`): |df0| from LINEAR to ZTF for modulated and unmodulated RRab.

## References

Blazhko 1907, Astron. Nachr. 175, 325. Buchler & Kolláth 2011, ApJ 731, 24. Donev & Ivezić 2025, AJ 169, 310 (arXiv:2504.05434). Jurcsik et al. 2009, MNRAS 400, 1006. LaCluyzé et al. 2004, AJ 127, 1653. Le Borgne et al. 2012, AJ 144, 39. Nowakowski & Dziembowski 2001, Acta Astron. 51, 5. Palaversa et al. 2013, AJ 146, 101. Sesar et al. 2011, AJ 142, 190. Shibahashi 2000, ASP Conf. Ser. 203 (the oblique pulsator model). Stothers 2006, ApJ 652, 643. Bellm et al. 2019, PASP 131, 018002. Masci et al. 2019, PASP 131, 018003. VanderPlas et al. 2012 (astroML).
