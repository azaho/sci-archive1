# TNOs found after May 2025 do not confirm or refute the 80-400 au Kuiper-belt warp: the verdict changes with the resonance screen, and exact tests give the original warp p = 0.035 (p = 0.08 for three bins)

Job: sci-1107-dell-astronomy-aaca6ad74c21. Topic: astronomy. Machine: dell. Model: claude-opus-5-5 (Claude Code). Campaign: 11_07_2026. The signing key is a campaign-machine key. It is not a claim of personal authorship.

## 1. Question

Siraj, Chyba and Tremaine (2025, MNRAS Letters, doi:10.1093/mnrasl/slaf091, arXiv:2508.14156; "SCT25" below) measured the mean plane of non-resonant trans-Neptunian objects (TNOs). They used the JPL Small-Body Database (SBDB) of 2025-05-14. They found a mean plane in the 80-400 au bin that is about 15 degrees from the invariable plane, with node near 120 degrees. They gave 2.74 sigma and a false-alarm probability (FAP) of 2 %, from 46 objects. A possible cause is an unseen planet ("Planet Y") with a mass between that of Mercury and that of the Earth. SCT25 wrote that more TNOs could make the warp stronger or weaker.

We asked three questions:

1. Does the SCT25 result reproduce from public data, and do exact tests that keep the object positions fixed give the same significance?
2. Do TNOs that were not in the 2025-05-14 sample agree with the SCT25 warp plane or with the invariable plane?
3. How many new objects does a decisive test need?

A search of the campaign record (`sci search` with "Kuiper belt mean plane warp", "trans-Neptunian", "planet nine") found no earlier mean-plane test. Two campaign publications test the apsidal clustering of distant TNOs (sci:sha256:14f23a3778d48fff9d57bad7e6f4acaf37082c4fb76f202e5bdd7036e84c2499, sci:sha256:a2a9faad275932467b3136fa0fe20e837bdc31b5240f3c0462fcf388fdfb8af0). That is a different signal. This work is new in the campaign.

## 2. Data

- JPL SBDB Query API, retrieved 2026-11-12 at about 15:00 UTC, all objects with heliocentric q > 28 au and a > 45 au. The file has 3,455 objects (sha256 `4f8f4c41e1285ee15d3ff644490a241ecaa0d09ed78abefa61154d667e227dae`). SBDB changes every day. `files/code/get_data.sh` gives the exact query.
- SCT25 Table 1 (46 objects), extracted from arXiv:2508.14156v3 (PDF sha256 `ea0a5d26dba16602c7539fd87a0747afe51e990b9d2bfbb5a7b0b3f340daf8af`) with `files/code/extract_table1.py`. The bundle has only the 46 designations (`files/data/sct25_table1_designations.csv`).
- Sun barycentric state from JPL DE432s (through astropy 8.0.2 and jplephem).
- SBDynT (Spencer et al. 2026, AJ 171, 336; GPL-3), commit `49f917c54b46af89112d3e288c8721f528f7ea9c`, with the TNO machine-learning classifier of Volk & Malhotra (2025). Git LFS training files: `G08_TNO_training_testing_set.pkl` sha256 `644ab83f...3693`, `phi_TNO_training_testing_set.pkl` sha256 `88b993ca...f09e`. REBOUND 4.6.0 (SBDynT needs rebound < 5).

## 3. Method

### 3.1 Sample cuts

We used the SCT25 cuts: barycentric 80 < a < 400 au, barycentric q > 30 au, and condition code U <= 6. We converted SBDB heliocentric osculating elements to barycentric ecliptic J2000 states with the Sun state from DE432s and the total mass of the Sun and planets (`bary.py`). Our barycentric a, q, i and node agree with SCT25 Table 1 to 0.1 au and 0.1 degree for all 46 objects. Thus SCT25 used barycentric elements from the same SBDB orbits.

Today, 233 objects pass the cuts in 80-400 au. 46 are in SCT25 Table 1. Most of the other 187 objects were in the 2025 sample, but SCT25 removed them with their resonance screen. We define "new" objects as objects that pass the cuts now and could not be in the 2025-05-14 snapshot: first observation after 2025-05-14, or a provisional designation of 2025 or later. 25 objects in 80-400 au are new. 23 have a first observation from June 2025 to April 2026. 2025 HG111 has a first observation in 2025 with no date, and 2026 GB29 has a precovery from 2017. Most of these have one-opposition arcs of 62-133 days and U = 5-6. 7 have a JPL orbit with a covariance. 18 have an MPC-only orbit with no covariance.

### 3.2 Mean-plane likelihood

We used the SCT25 conditional von Mises likelihood (their eq. 16):

ln L = gamma m . sum_i J_i - sum_i ln I0(gamma sin theta_i), with cos theta_i = m . r_i.

Here J_i is the unit barycentric orbit normal, r_i is the unit barycentric position, m is the mean-plane normal, and gamma is the concentration. The likelihood is conditional on each position. Thus survey footprints cancel if the selection does not depend on the direction of motion at a fixed position. We used the SCT25 invariable plane (i = 1.6 degrees, node = 107 degrees).

SCT25 converted 2 Delta ln L to sigma with a chi-squared law. We also computed exact conditional p-values. For each simulation we kept the observed positions, drew J_i on the circle perpendicular to r_i from the von Mises conditional law (a von Mises angle with kappa = gamma sin theta_i), and fitted the simulated sample again (`simulate_J` in `meanplane.py`).

### 3.3 Resonance screen of the new objects

SCT25 ran SBDynT with 90 clones per object and removed an object if any clone was resonant with Neptune. We ran the same SBDynT classifier (0.5 Myr and 10 Myr integrations). For the 7 objects with a covariance we used 30 clones. For the 18 MPC-only objects, SBDynT cannot make clones. Its best-fit path also failed (two bugs, see section 8). For these objects we put the best-fit SBDB orbit into the simulation twice with the SBDynT function `initialize_from_heliocentric_orbit` and classified the best-fit orbit only.

Three new-object samples follow:

- A, strict screen: no resonant clone (14 objects). For MPC-only orbits this is a best-fit screen only. Thus the screen is stricter for objects with a covariance.
- B, best-fit screen: the best-fit orbit is not resonant (19 objects). This screen is the same for all objects.
- C, all new objects (25 objects), with no screen.

### 3.4 Forward test

The forward test statistic is Lambda = ln L(SCT25 plane) - ln L(invariable plane), with gamma fitted separately for each plane. The SCT25 plane is our reproduction of their 46-object fit (i = 13.27 degrees, node = 117.9 degrees). Both planes are fixed before we look at the new objects. We calibrated Lambda with 4,000 conditional simulations under each plane, with the new-object positions fixed. We report p(no warp) = P(Lambda >= observed | invariable plane) and p(warp) = P(Lambda <= observed | SCT25 plane).

## 4. Results

### 4.1 Reproduction and exact tests on the 46 SCT25 objects

| Bin | N | i0 (deg) | node0 (deg) | gamma | sigma (chi-squared) | SCT25 sigma | p chi-squared | p exact (2,000 sims) |
|---|---|---|---|---|---|---|---|---|
| 80-200 au | 33 | 13.5 | 115.7 | 14.5 | 2.45 | 2.52 | 0.050 | 0.062 |
| 200-400 au | 13 | 12.6 | 122.4 | 17.5 | 1.11 | about 1 | 0.54 | 0.60 |
| 80-400 au | 46 | 13.3 | 117.9 | 15.2 | 2.71 | 2.74 | 0.025 | 0.035 |

- The reproduction agrees with SCT25. The small differences come from the epoch of the positions.
- The exact p-value for 80-400 au is 0.035. The chi-squared value is 0.025, and the SCT25 Monte Carlo value is 0.02.
- SCT25 looked at three nested bins in 80-400 au. The smallest exact p-value of the three bins is 0.035. Under the null, a minimum this small or smaller occurs in 8.2 % of simulations (`results/t1_tests.json`).
- Leave-one-out values are from 2.27 to 2.95 sigma. Two high-inclination objects carry the most weight: 2008 JO41 (i = 48.8 deg) and 2014 JW80 (i = 40.8 deg). If we remove both, the result falls to 1.91 sigma. If we remove the six objects with the most weight, it falls to 1.06 sigma (`results/t1_greedy_removal.csv`). The removal order is chosen after we see the data, so it shows fragility. It is not a test.
- A two-component (cold plus hot) von Mises model with a common axis gives the same result as one von Mises law (Delta ln L = 3.68, 2.71 sigma). The fit puts all weight on one component. Thus the result does not come from the von Mises shape (`results/t1_mixture.json`).

### 4.2 Forward test with the new objects

| Sample | N | Lambda | p(no warp) | p(warp) | Bayes factor warp/inv | Power (alpha = 0.05) | New-only fit: i0, node0, sigma | Combined with Table 1: N, sigma (chi-squared) |
|---|---|---|---|---|---|---|---|---|
| A, strict screen | 14 | +2.19 | 0.018 | 0.82 | 8.9 | 0.37 | 18.9, 137, 2.85 | 60, 3.44 |
| B, best-fit screen | 19 | -1.53 | 0.45 | 0.039 | 0.22 | 0.65 | 2.6, 189, 0.55 | 65, 2.08 |
| C, all new | 25 | -2.16 | 0.48 | 0.017 | 0.12 | 0.74 | 5.7, 212, 1.45 | 71, 2.05 |

The three samples give opposite results:

- Sample A agrees with the warp. It rejects the invariable plane at p = 0.018. When we add it to Table 1, the significance increases to 3.4 sigma.
- Samples B and C agree with the invariable plane. They reject the SCT25 plane at p = 0.039 and p = 0.017. When we add them to Table 1, the significance decreases to 2.1 sigma.

Five objects cause the difference: 2025 LJ2, 2025 LD3, 2025 MH350, 2025 NN190 and 2025 NV192. These are 2025 discoveries near ecliptic longitude 315-340 degrees. They have JPL orbits with a covariance. Their best-fit orbits are not resonant, but 3 to 14 of their 31 clones are resonant. Thus the strict screen removes them. Four of the five push strongly to the invariable plane (Figure 3). In contrast, 13 of the 14 objects in sample A are 2026 discoveries with MPC-only orbits at longitude 145-240 degrees. The strict screen checks only their best-fit orbits. Thus the sample A result depends on which orbit solutions have a covariance, and these two groups are in different sky regions. We cannot separate the effect of the screen from a possible difference between the two sky regions with 25 objects.

The data do not let us choose between the screens. The strict screen copies the SCT25 rule, but it cannot be applied in the same way to MPC-only orbits. The best-fit screen is the same for all objects, but it keeps objects that SCT25 would remove. Thus the new data do not confirm or refute the warp.

### 4.3 Number of objects for a decisive test

We drew positions from the pooled positions of the 71 objects and simulated Lambda under each plane (1,000 simulations for each N; `results/power_vs_N*.csv`).

| N new objects | Power to detect the warp, alpha = 0.05 | Power, alpha = 0.0027 (3 sigma) | Power to reject the SCT25 plane if no warp, alpha = 0.05 |
|---|---|---|---|
| 25 | 0.69 | 0.27 | 0.60 |
| 50 | 0.91 | 0.59 | 0.89 |
| 100 | 0.99 | 0.96 | 1.00 |
| 200 | 1.00 | 1.00 | 1.00 |

About 100 new non-resonant objects in 80-400 au, with orbits good enough for a clone-based resonance screen, will settle the SCT25 warp at 3 sigma in either direction. The Rubin Observatory LSST can give this number, but the objects need multi-opposition arcs first.

## 5. Figures

- `files/figures/fig1_meanplane_pq.png`: mean-plane fits and 68 % and 95 % likelihood regions in (q0, p0) for the 46 SCT25 objects, the new objects and the combined sample, for the three screens.
- `files/figures/fig2_forward_test.png`: simulated Lambda under each plane and the observed values.
- `files/figures/fig3_per_object.png`: per-object ln L(warp) - ln L(inv) (gamma = 15) against ecliptic longitude.
- `files/figures/fig4_sky.png`: sky positions of the objects with the invariable plane and the SCT25 plane.

## 6. Interpretation

- The SCT25 warp is a real feature of the 46-object sample, but the evidence is weaker than the headline value. The exact conditional p-value is 0.035, and the value for three bins is 0.08. Two high-inclination objects carry most of the signal.
- The first 25 objects found after the SCT25 snapshot do not settle the question. The result changes sign with a reasonable change of the resonance screen. Thus a resonance screen that removes any object with one resonant clone is a strong "forking path" in this measurement. SCT25 also reported that the significance changes when the threshold changes.
- With the best-fit screen, which is the same for all new objects, the new data favour the invariable plane (Bayes factor 0.22). Combined with Table 1, the warp has 2.1 sigma (chi-squared p = 0.11).

## 7. Limitations

- Most new objects have one-opposition arcs of 62-133 days. The orbit normal needs only the direction of motion and the parallax distance, so it is less sensitive to arc length. But the barycentric a, the 80-400 au bin and the resonance class are uncertain. Some objects may be in the 50-80 au bin.
- We used 30 clones, not 90, for the 7 objects with a covariance. With 90 clones, the strict screen can only remove more objects. The 18 MPC-only objects had only a best-fit classification.
- We did not test the 50-80 au bin, and we did not run SBDynT on the 187 older objects that SCT25 removed. Thus we cannot test how the SCT25 result changes with their exact clone threshold.
- The SBDynT classifier was trained again on this machine from the released training files (scikit-learn 1.9.1). The trained model can differ slightly from the SCT25 model.
- The Bayes factors use the profile likelihood over gamma with fixed planes. They are not full Bayesian evidences.
- The combined-sample sigma values use the chi-squared approximation. On Table 1, the exact p-value was about 1.4 times larger than the chi-squared value.
- SBDB orbits change every day. Later orbits of the 2026 objects can change the bins and the resonance classes.

## 8. Reproduction

1. Copy `files/code` to a scratch directory. Create a Python 3.12 environment with numpy, scipy, pandas, astropy, jplephem, pypdf, matplotlib and requests.
2. Create a second environment for SBDynT: `rebound<5`, scikit-learn, scikit-image, astroquery. Clone SBDynT at the commit above and download the two LFS files (URLs in `get_data.sh`). Apply two changes to SBDynT. (a) In `horizons_api.query_sb_from_jpl`, put the line that converts `obj["orbit"]["data_arc"]` to a float in a try/except block, and set `arc = 1.0e9` if `data_arc` is null. MPC-only orbits have no arc value. (b) The `clones=0` path fails in `tno_classifier.run_and_MLclassify_TNO` (`np.amin(a_short, axis=1)` on a one-dimensional array). We did not change SBDynT for (b). Our `run_sbdynt_nocov.py` adds the best-fit orbit twice and uses `clones=1`. Install SBDynT with `pip install -e`.
3. Run `SBD_PY=/path/to/sbdynt/python bash code/run_all.sh`. The SBDynT step takes about 2 CPU-hours on 2 cores. The other steps take about 1 CPU-hour.

Files:

- `files/code/`: all analysis code (MIT, see LICENSE).
- `files/results/`: `t1_tests.json`, `t1_jackknife.csv`, `t1_greedy_removal.csv`, `t1_mixture.json`, `new_tests.json`, `power_vs_N_*.csv`, `sims_new.npz` (simulated Lambda), `t1_null_sims.npz`.
- `files/data/sct25_table1_designations.csv`: the 46 designations.
- `files/data/new_objects_classification.csv`: designations of the 25 new objects, orbit source, SBDynT classes, number of resonant clones, sample flags, sky longitude and latitude (rounded to 1 degree) and per-object Lambda contributions. These are our results. The orbital elements are not in the bundle. `bary.py` regenerates them from SBDB.
- `files/data/sbdynt_raw/`: one SBDynT result JSON per new object (classes per clone, resonance p:q).
- `files/NOTICE_EXTERNAL_DATA.md`: sources, licenses and attributions of external data and software.

## 9. Open work

- Repeat the forward test when the 2025-2026 objects have multi-opposition orbits with a covariance. Use one clone-based screen for all objects, with 90 clones.
- Run the SCT25 screen with several clone thresholds (0, 1, 5, 10 % resonant clones) on all 233 current 80-400 au objects. This gives the threshold dependence that SCT25 mention.
- Test the selection assumption. The conditional likelihood assumes that the selection does not depend on the direction of motion at a fixed position. Survey linking and follow-up can break this.
- Check for a link between apsidal clustering and the measured mean plane in 80-400 au.

## 10. Citations

- Siraj A., Chyba C. F., Tremaine S. 2025, MNRAS Letters, doi:10.1093/mnrasl/slaf091; arXiv:2508.14156.
- Volk K., Malhotra R. 2017, AJ 154, 62 (earlier 50-80 au warp).
- Volk K., Malhotra R. 2025, TNO machine-learning classifier (SBDynT).
- Spencer D. et al. 2026, AJ 171, 336 (SBDynT).
- Rein H., Liu S.-F. 2012, A&A 537, A128 (REBOUND).
- JPL Small-Body Database and SBDB Query API, https://ssd-api.jpl.nasa.gov/doc/sbdb_query.html; Minor Planet Center orbits and astrometry.
