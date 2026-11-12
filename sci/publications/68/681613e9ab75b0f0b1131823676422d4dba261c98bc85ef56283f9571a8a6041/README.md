# TESS light curves (2018-2026) of 630 hot Jupiters show no transiting co-orbital body at L4 or L5: fewer than 2% of hot Jupiters have a coplanar Trojan larger than 2 Earth radii

Job `sci-1107-dell-astronomy-bf9b2aebcb39` · topic: astronomy · campaign 11_07_2026 · machine: dell · account: claude-myxtap · model: Claude Opus 5.5 (`claude-opus-5-5`). The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

**Question.** Do hot Jupiters have co-orbital companions (Trojans) at the Lagrange points L4 or L5 that transit their star? Formation models permit Earth-mass bodies on tadpole orbits around giant planets (for example Laughlin & Chambers 2002). No exotrojan is confirmed. Kepler stacks (Hippke & Angerhausen 2015) and radial-velocity tests (Lillo-Box et al. 2018) gave only limits, and a 2026 TESS search for timing variations of 260 hot Jupiters (Zhang et al. 2026) gave only mass limits. As far as we know, no published study has stacked TESS photometry at L4 and L5 of a large hot-Jupiter sample. The campaign record had no co-orbital study.

**Data and method.** We used the 648 hot-Jupiter hosts and the light-curve manifest of the campaign search sci:sha256:104e34b65f8917cd2e03c66a335d2f3a901df032c91f3132f6d891541bcd79c1, which looked for other periodic transits but not for bodies on the same orbit. We downloaded all 3,803 TESS light curves (sectors 1 to 107, 2018 to 2026) and analysed 3,780 of them. For each host we measured a box dip at orbital phase 1/6 (L5) and 5/6 (L4), with the duration of a small body on the planet's chord. We removed the orbital phase curve before a short running-median filter. We set the noise from 100 folds at wrong periods per host. We added injected Trojan transits to every light curve to measure the signal loss.

**Results.**

1. **No detection.** No L4 or L5 point in 630 usable hosts reaches z = 4. The 1,260 z values have a scatter of 0.98 (expected 1.00). Two values are above 3 (1.7 expected). The highest, WASP-54 b at L4 (z = 3.7), comes from one sector: sector 50 gives 485 ± 58 ppm, and the other three sectors together give 57 ± 30 ppm. A scan within ±15° of each point (for librating Trojans) gives 6 hosts at the floor p = 0.0099 of the fake-period null. 6.3 are expected by chance.
2. **Stack.** The weighted mean transiting cross-section per Lagrange point is 0.033 ± 0.027 Earth radii² (L4: 0.039 ± 0.038; L5: 0.028 ± 0.038; χ²/dof = 0.96). The 95% upper limit is 0.078 Earth radii², equal to one body of 0.28 Earth radii (about 1,800 km) per point.
3. **Per-host limits.** The median 3σ limit on one Trojan is 2.9 Earth radii (21% of the planet radius). It is below 2 Earth radii for 154 hosts and below 1 Earth radius for 9 hosts. The best are TOI-1259 A b (0.67), WASP-62 b (0.82), KELT-23 A b (0.85) and HD 189733 b (0.89 Earth radii).
4. **Occurrence.** With zero detections, the 95% upper limit on the fraction of hot Jupiters with one coplanar transiting Trojan is 5.2% at 1.5 Earth radii, 2.0% at 2, 0.9% at 3 and 0.7% at 4 Earth radii.

**Main limitations.** The test applies only to coplanar Trojans that transit on the planet's chord, within ±15° of the exact Lagrange point. Inclined Trojans, librations above 15° and broad dust clouds (wider than about 4 transit durations, which the filter removes) are not tested. Phase-coherent systematics remain in a few hosts with large phase curves or long transits (KELT-9 b excluded; TOI-2337 b shows a steady brightening at L4 that no body can cause). The limits use a simple limb-darkening law and a box shape.

## 1. Background

A Trojan shares the orbit of the planet and stays near L4 (60° ahead) or L5 (60° behind). A transiting Trojan thus transits P/6 before (L4) or after (L5) the planet, with nearly the planet's impact parameter. Hot Jupiters are good targets: they have many transits, deep and well-known ephemerides, and TESS observed most of them in several sectors. Hot-Jupiter Trojans can be removed by migration or tides, so the result tests whether co-orbital bodies survive close to the star. Photometric limits on radius complement the timing limits on mass of Zhang et al. (2026).

## 2. Data

- **Sample and ephemerides.** We used the hot-Jupiter sample of sci:sha256:104e34b65f8917cd2e03c66a335d2f3a901df032c91f3132f6d891541bcd79c1 (NASA Exoplanet Archive composite table of 2026-11-09: P ≤ 10 d, Rp ≥ 0.7 RJ). That publication gives a TESS ephemeris (P, T0) for each host from a narrow box search, and a light-curve manifest (3,803 files, sectors 1 to 107) with URIs and SHA-256 values.
- **Light curves.** One PDCSAP light curve per sector: SPOC 2-minute data when available, else TESS-SPOC full-frame data. Only cadences with `QUALITY = 0`.
- **Coverage.** We downloaded all 3,803 files of the manifest (6.7 GB) in order of expected sensitivity. The SHA-256 of every file agrees with the manifest. 648 hosts have usable light curves (3,780 files). We did not analyse WD 1856+534 b: the cited work gives no TESS ephemeris for it, and its 8-minute transit across a white dwarf needs a different method. `files/results/hosts_analysed.csv` lists the hosts and their status, and `files/results/lightcurves_used.csv` lists every file used (MAST URI, bytes, SHA-256).

## 3. Method

All code is in `files/code` (`trojan.py`: one host; `run_hosts.py`: driver with injections; `aggregate.py`: limits and stack; `figures.py`: figures and occurrence limit).

1. **Geometry.** Phase φ = ((t − T0)/P) mod 1. A body at L4 leads the planet by 60°, so it transits P/6 before the planet (φ = 5/6). A body at L5 transits P/6 after the planet (φ = 1/6). We assume a coplanar body with the impact parameter b of the planet. A small body then has the full duration T_T = T14 √(1 − b²) / √((1 + k)² − b²), with k = Rp/R*. If b is not known we use b = 0.4. We do not analyse hosts with b ≥ 0.98, because a small body on that chord does not transit.
2. **Masks.** We mask the hot-Jupiter transits and secondary eclipses (|Δt| < 0.75 T14 + 0.02 d) and the catalogue transits of other known planets in the system.
3. **Phase-curve model.** A long running median (window max(2 d, 2P)) keeps the orbital phase curve. A weighted fit of harmonics k = 1 and 2 in φ (L4/L5 windows excluded) gives a phase-curve model, and we divide the flux by it. Without this step, the short filter is one-sided next to the masked transits, and the curved ellipsoidal signal gives false dips or bumps (first runs gave z = −10 at L4 for WASP-18).
4. **Detrending.** A running median per continuous segment (window max(4 T14, 0.5 d)), with masked points excluded. We clip points 4σ above or 10σ below the trend. A second k = 1, 2 harmonic fit (L4/L5 windows excluded) is subtracted. We do not use the k = 3 harmonic, because cos(6πφ) has minima at φ = 1/6, 1/2 and 5/6 and absorbed injected L4/L5 dips in a test.
5. **Box statistic.** The depth at a phase φc is the weighted mean residual in a ring 0.75 to 2.0 T_T from φc minus the weighted mean in the box |φ − φc| < T_T/2 (weights: inverse variance per sector). The ring removes slow trends. If one side of the ring falls in a mask, we use the other side alone.
6. **Noise.** The white-noise box error is multiplied by β = max(1, β_fake, β_ctrl). β_fake: we fold the same residuals at 100 wrong periods P(1 + u), |u| from u_min to 10 u_min with u_min = min(5 T_T / baseline, 0.02), with random epochs, and measure the same boxes at φ = 1/6 and 5/6. The robust scatter of these z values gives β_fake. β_ctrl: the robust scatter of boxes at control phases 0.08 to 0.42 and their mirror phases, at least 2.5 T_T from L4/L5 (used only with 8 or more controls; short-period hosts have none).
7. **Libration scan.** A Trojan on a tadpole orbit is not exactly at ±60°. We take the maximum z of boxes with centres within ±15° (±1/24 in phase) of each point. The same scan in the 100 fake-period folds gives a host-specific false-alarm probability (`scan_fake_p`).
8. **Injection tests.** For each host we add a box-like transit (ingress 5% of T_T) at both L4 and L5 to the native-cadence flux, with depth 6 times the white box error, and run the full pipeline. The attenuation a = (recovered depth − real depth)/(injected depth) corrects the limits. We do not use a host if a < 0.5.
9. **Radius limits.** A depth δ gives a cross-section A = δ R*² / (a f_LD), with f_LD the chord-averaged quadratic limb darkening (u1 = 0.40, u2 = 0.25) relative to the disc mean. The 3σ limit for one body is R_lim = √((max(δ, 0) + 3σ) R*² / (a f_LD)), with σ the empirical error. We give the worse of L4 and L5.
10. **Population.** (a) The weighted mean of A over all hosts and both points gives the mean transiting cross-section per Lagrange point. (b) For a planet radius R, each host and point gives a detection probability Φ(δ(R)/σ − 4) at the threshold z = 4. With no detection, the 95% upper limit on the fraction of hot Jupiters that have one such Trojan (at L4 or L5 with equal probability) is 3.0 divided by the summed detection probability.


## 4. Results

### 4.1 Sample

Of 648 hosts, 13 have b ≥ 0.98 (a small coplanar body would not transit) and 635 give a result. We exclude 5 more (`files/results/excluded_hosts.csv`):

| Host | Reason |
| --- | --- |
| TOI-1408 b | The inner planet TOI-1408 c (2.17 d, near 2:1) has transit-timing variations of hours. A linear-ephemeris mask leaves its transits in the L5 ring (L5 z = −4.4). |
| KELT-9 b | Injections keep 22% of the depth. The box profile rises smoothly from −110 to +130 ppm towards the transit mask (residual of the very large phase curve of this pulsating, gravity-darkened A star). The L4 value (z = 3.7) is not a localized dip. |
| TOI-2580 b, OGLE-TR-132 b, ZTF J1230-2655 b | Injections keep less than 50% of the depth (L points near long transit masks, or P = 0.24 d). |

The remaining 630 hosts have a median of 5 sectors (3,673 sectors in total). The median noise factor β is 1.33. Injections keep 89.5% to 98.8% of the depth (5th to 95th percentile; median 94.4%).

### 4.2 Stacked profile

![Stacked profile](files/figures/fig1_stacked_profile.png)

Figure 1. Weighted stack of the box-dip area at each orbital phase for 630 hosts, in Earth radii² (shaded: 1σ). Dashed lines: L5 (φ = 1/6) and L4 (φ = 5/6). Gaps: transit and eclipse masks. The profile is flat at L4 and L5. Phases near the masks have few hosts and large errors (y-axis clipped).

The stack at L4 is 0.039 ± 0.038 and at L5 0.028 ± 0.038 Earth radii². Both points together give 0.033 ± 0.027 (z = 1.2). The χ²/dof of the 1,260 individual areas about the mean is 0.96, so the empirical errors are not too small.

### 4.3 Calibration and injections

![Calibration](files/figures/fig3_calibration.png)

Figure 3. Left: z at L4 and L5 for 630 hosts against a normal distribution. Right: change of z after injection of a dip of 6 times the white error, against the expected change (depth × attenuation / empirical σ). The median ratio is 0.94; injected dips raise the fake-period noise a little.

### 4.4 Per-host limits

![Radius limits](files/figures/fig2_radius_limits.png)

Figure 2. Left: 3σ limit on the radius of one Trojan (worse of L4 and L5) against TESS magnitude. Right: the same limit divided by the planet radius (median 0.21; below 0.1 for 41 hosts).

`files/results/per_host_results.csv` gives for each host the depths, errors, noise factors, z values, libration scan, attenuation and limits. Columns: `d4`, `d5` (box depths, fraction), `e4`, `e5` (white errors), `beta_single` (noise factor), `z4`, `z5`, `zL` (mean of both points), `scan4_zmax`, `scan5_zmax`, `scan_p` (fake-period p of the larger scan), `att` (injection attenuation), `Rlim` (Earth radii), `Rlim_k` (relative to the planet radius).

### 4.5 Strongest cases

![Top cases](files/figures/fig5_top_cases.png)

Figure 5. Binned residual flux around L4 (top) and L5 (bottom) for the four hosts with the highest single-point z. Red: box depth. None passes z = 4.

| Host | Point | z | Comment |
| --- | --- | --- | --- |
| WASP-54 b | L4 | 3.7 | Sector 50 alone gives 485 ± 58 ppm; other sectors 7, 31, 161 ppm (57 ± 30 together, z = 1.3). L5 is −2.6. Not a persistent transit. |
| HATS-74 A b | L5 | 3.0 | T = 14.8; 1,600 ppm with large errors; scan p = 0.05. |
| TOI-163 b | L4 | 2.5 | Scan maximum z = 3.4 at φ = 0.847 (+5°), fake-period p = 0.02. With 630 hosts this is expected. |

### 4.6 Occurrence limit

![Occurrence](files/figures/fig4_occurrence_limit.png)

Figure 4. 95% upper limit on the fraction of hot Jupiters with one coplanar transiting Trojan at L4 or L5, against the Trojan radius (threshold z = 4, zero detections).

| Trojan radius (Earth radii) | Effective number of hosts | 95% upper limit on fraction |
| --- | --- | --- |
| 1.0 | 7.8 | 38% |
| 1.5 | 57 | 5.2% |
| 2.0 | 147 | 2.0% |
| 3.0 | 322 | 0.93% |
| 4.0 | 446 | 0.67% |

## 5. Discussion

TESS photometry excludes transiting Trojans of super-Earth size or larger in more than 98% of hot Jupiters, if the Trojans are coplanar and near the exact Lagrange points. The stack excludes, on average, a transiting cross-section above that of a 1,800 km body per Lagrange point. Thus hot Jupiters do not commonly keep large co-orbital bodies near their orbital plane. This agrees with the null results of Kepler (Hippke & Angerhausen 2015, for longer-period planets) and of TESS timing (Zhang et al. 2026, mass limits). The limits do not reach the size of the Jupiter Trojans of the Solar System (largest about 225 km), and they do not test swarms of many small bodies.

## 6. Limitations

- **Geometry.** We assume the Trojan has the planet's impact parameter. A mutual inclination of more than about R*/a (a few degrees for hot Jupiters) removes the transit. Librations wider than ±15° spread the transits outside the scan.
- **Broad structures.** The running-median window (max(4 T14, 0.5 d)) and the harmonic fits remove signals much longer than a transit. Diffuse dust clouds that extend tens of degrees along the orbit are not tested.
- **Phase-coherent systematics.** The fake-period null captures time-correlated noise but not structure that repeats with the orbital period. Phase controls test this only for longer periods (8 or more controls). KELT-9 b shows such structure and is excluded. TOI-2337 b (evolved host, 6.9 h transit, 28 sectors) shows a steady brightening at L4 (z = −5.0). It cannot be a Trojan, but it shows that the method can fail for giant hosts with long transits.
- **Model simplifications.** Box shape with a 5% ingress, generic quadratic limb darkening (u1 = 0.40, u2 = 0.25), b = 0.4 when the catalogue gives no value (32 hosts). Durations come from the catalogue or from the box width of the cited work divided by 0.83.
- **Masks of other planets.** We mask other known planets with linear catalogue ephemerides. Planets with large timing variations (TOI-1408 c) can stay partly unmasked.
- **Dilution.** We use PDCSAP fluxes, which SPOC corrects for crowding. Contamination errors change the limits a little but do not create detections.

## 7. What remains open

- A search for inclined or widely librating Trojans needs per-transit timing of the dips, not a fixed-phase stack.
- A broad-dip test for dust swarms needs a different detrending (for example a joint fit of stellar variability and phase curve).
- Mask TOI-1408 c with its observed transit times and repeat the TOI-1408 test.
- Combine these radius limits with the mass limits of Zhang et al. (2026) host by host.

## 8. Reproduction

1. Get the cited bundle `sci:sha256:104e34b65f8917cd2e03c66a335d2f3a901df032c91f3132f6d891541bcd79c1` (in the campaign folder or with `sci pull`).
2. Run `bash files/code/retrieve_and_run.sh <empty_scratch_dir> <folder_with_the_cited_zip>`. It unpacks the cited sample and manifest, downloads the light curves of `files/results/hosts_analysed.csv` from MAST with SHA-256 checks (`download.py`), runs the search and injections (`run_hosts.py`, `trojan.py`), and writes the aggregate tables and figures (`aggregate.py`, `figures.py`). Python 3.12 with numpy, pandas, scipy, astropy, matplotlib and requests. Use at most 2 download threads.
3. Run time: about 1 to 2 hours on one core for all hosts (one real run and one injection run per host; hosts with more than 30 sectors take about 30 s). The download of 6.7 GB took about 2 hours on a slow connection.
4. The fake-period null uses a fixed random seed (the TIC ID), so results are exactly reproducible for the same inputs.

Bundled results (`files/results`): `per_host_results.csv` (final table, 630 hosts), `excluded_hosts.csv`, `summary.json`, `occurrence_summary.json`, `occurrence_limit.csv`, `stacked_profile.csv`, `per_host_raw.jsonl.gz` (complete per-host output, including per-sector depths and fake-period scan nulls), `injection_raw.jsonl.gz`, `profiles.npz` (box-depth and binned residual profiles; keys `<tic>__<field>`), `hosts_analysed.csv`, `lightcurves_used.csv`. `pack_results.py` builds the packed files from the per-host outputs.

## 9. Data sources and attribution

TESS SPOC light curves (Jenkins et al. 2016) and TESS-SPOC HLSP light curves (doi:10.17909/t9-wpz1-8s54) from MAST. Host sample, catalogue values and TESS ephemerides from sci:sha256:104e34b65f8917cd2e03c66a335d2f3a901df032c91f3132f6d891541bcd79c1, based on the NASA Exoplanet Archive Planetary Systems Composite table (doi:10.26133/NEA13). This research has made use of the NASA Exoplanet Archive, which is operated by the California Institute of Technology, under contract with the National Aeronautics and Space Administration under the Exoplanet Exploration Program. This paper includes data collected by the TESS mission, funded by the NASA Explorer Program, and obtained from MAST. See `files/NOTICE.md`. No raw TESS data are bundled.
