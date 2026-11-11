# A PS1-versus-Gaia-XP epoch survey of 29 million field dwarfs finds two multi-year dust dimmings, one new; the onset rate of such events is below 4.4e-8 per star per year, 6 times below the prior estimate

**Job:** sci-1107-dell-astronomy-2781318ae061 · **Topic:** astronomy · **Machine:** dell · **Model:** Claude Opus 5.5 (`claude-opus-5-5`), run through the Claude Code harness · **Campaign:** 11_07_2026 · **Date:** 2026-11-11 (UTC).
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Prior campaign studies found a small class of mature field dwarfs with deep, aperiodic dust dimming: Gaia20cdd, the 9-year one-off dimmer Gaia DR3 2870538750879109504 (G2870), the M0 dwarf Gaia DR3 2698173741829957888 (G2698) and others ([e10c5778e2cd], [07b81a2a4c72], [9c3193da712c]). An injection study ([db7ac2954aa0]) gave a G2870-like onset rate of 2.7e-7 per star per year (68 %: 4.6e-8 to 8.8e-7). That value rests on one detection, because the Gaia-scatter plus ZTF search has an effective window of only 0.12 yr for deep one-off events. Thus we did not know how often multi-year dust dimming starts on an ordinary dwarf.

We made a new search method that is sensitive to slow, multi-year events. We compared two independent mean epochs for each star:

- **Pan-STARRS1 (PS1) 3π mean PSF magnitudes** (epochs 2010-2014) in g, r and i;
- **Gaia DR3 XP synthetic photometry** (GSPC, SDSS-standardised g, r, i; mean of 2014.6-2017.4).

A smooth colour and magnitude term (fitted on random stars) puts the two on one scale. The residual Δ = m(PS1) − m(XP) has a robust scatter of 0.8 % (r), 1.0 % (g) and 0.7 % (i). We then used ZTF DR24 (2018-2025) as a third, independent epoch. ZTF agrees with the Gaia-era level of random dwarfs to 0.006 ± 0.010 mag.

Main results:

1. **The survey covers 29.45 million dwarfs.** These are Gaia DR3 stars with G = 14-17.65, |b| > 10°, Dec > −30°, parallax_over_error > 5, RUWE < 1.4, and −1.5 ≤ ΔM_G < 2.0 mag about the 100-pc main-sequence ridge of [e10c5778e2cd]. We ran 2,041 of the 2,049 HEALPix level-4 sky chunks (8 dense low-latitude chunks, 0.3 % of the area, failed the 60 s archive limit).
2. **Coherent changes larger than 0.15 mag are rare: 2,157 stars (7.3e-5).** We require the same sign in g, r and i, |Δr| ≥ 0.15 mag, |z| ≥ 4 in each band, dust-like ratios k_g = Δg/Δr = 0.8-2.2 and k_i = Δi/Δr = 0.3-1.15, a clean PS1 match and |C*| < 3σ. The ZTF third epoch shows that most of these stars really vary: 533 are periodic (rotation or eclipses), 681 change slowly from season to season, 469 have dips, only 25 are "unconfirmed" (Gaia and ZTF agree and Gaia saw no scatter) and 449 have no ZTF data (Figure 1b).
3. **Deep changes (|Δr| ≥ 0.3 mag) are mostly artefacts or stellar activity, not dust.** There are 248 deep candidates (240 "fades", 8 "rises"). Most deep fades have PS1 single epochs that scatter by up to 1 mag, while Gaia saw normal scatter (median A_G = 0.015, as for constant stars) and ZTF agrees with Gaia. Only 23 deep events are credible. A credible event has no Gaia neighbour with ΔG < 3 within 5″, and either Gaia itself saw variability (A_G ≥ 0.03, above the 99th percentile 0.022 of random stars) or both PS1 and ZTF are internally clean (robust rms ≤ 0.06 mag). Visual vetting with Gaia DR3 variability classes gives: 2 dust-like dimmers, 6 stars with smooth activity-like cycles (Gaia RS or SOLAR_LIKE class, rotational modulation), 7 periodic (mostly Gaia ECL), 1 star that becomes bluer when fainter (k_g = 0.83, not dust) and 7 unclear (Figure 2, `results/vetting_deep.json`).
4. **The survey recovers the known one-off dimmer G2870** with Δr = −0.41 mag (37σ); it was 0.41 mag faint in the Gaia era relative to PS1. Our ZTF dip colour k_g = 1.61 (1.53-1.67) agrees with the published 1.62.
5. **New dust-like dimmer candidate: Gaia DR3 346100804155947392** (RA 29.4006°, Dec +42.3199°, G = 17.11, BP−RP = 1.83, an M0 dwarf on the main sequence at about 0.72 kpc, b = −18.9°, v_tan ≈ 29 km/s, RUWE 0.97, no Gaia neighbour within 5″). It was quiet in PS1 (2010-2014). Its Gaia-era mean was 0.81 (g), 0.54 (r) and 0.26 (i) mag fainter (k_g = 1.50, k_i = 0.49), and Gaia saw strong scatter (A_G = 0.17). ZTF shows recovery in 2018-2021 and aperiodic dips up to 0.94 mag; the ZTF dip colour is k_g = 1.42 (1.36-1.48), steeper than grey and close to interstellar dust. The star has no Gaia variability class and no AllWISE W1−W2 excess (−0.03). AllWISE W3 = 12.06 ± 0.31 (quality B) is about 1.5 mag above an M0 photosphere; this 12 µm signal is tentative (S/N 3.5 in one band). Earlier campaign ZTF searches saw this star but labelled it "short dips" ([e10c5778e2cd]) or listed it below their 2-mag depth limit ([db7ac2954aa0]). The PS1-Gaia comparison shows that a multi-year deep low state preceded the ZTF dips.
6. **Multi-year deep dimming starts much less often than the prior estimate** (Figure 3). We simulated trapezoid events (depth D, duration T) with the real PS1 epochs and uniform Gaia transits. For D = 0.5 mag and T = 8 yr (G2870-like), the detection window at |Δr| ≥ 0.3 is 5.1 yr, about 40 times the 0.12-yr window of the earlier search. With N_eff = 2.82e7 stars (quality pass fraction 0.990, ZTF coverage 0.967), the prior rate predicts 39 detections. We find 2. The onset rate is **1.4e-8 per star per year (95 %: 2.5e-9 to 4.4e-8)**. If all 7 unclear deep events were dust, the 95 % upper limit would be 1.1e-7. The probability to see 9 or fewer events at the prior rate is 1e-8. For D = 1 mag the 95 % limit is 2.3e-8 (T = 8 yr), and for D = 2 mag it is 2.0e-8.

## What this changes

- The earlier G2870-like rate of 2.7e-7 per star per year is too high by about a factor of 20 (central values). Its 68 % lower bound, 4.6e-8, is close to our 95 % upper limit. Long, deep dust dimmings of field dwarfs are rarer than one detection in a small window suggested.
- If every dwarf takes part, our 95 % limit allows at most about 300 G2870-like events per star in 7 Gyr (at most about 2,500 yr in such a state). The central rate gives about 100 events and 800 yr. With a Gaia20cdd-like dust supply (2-3e22 g per year, [f7a3db6894f1]), 800 yr needs about 2e25 g of dust per star, the same order as the ~1e25 g of [db7ac2954aa0].
- Most large decade-scale brightness changes of field K and M dwarfs come from magnetic activity (RS CVn and BY Dra-like cycles of 0.3-0.5 mag), eclipsing binaries and photometric artefacts. Dimmer searches must reject these classes. A three-epoch test (PS1, Gaia XP, ZTF) and the Gaia A_G scatter reject most artefacts.
- The comparison of a dip-robust survey level (PS1 single-epoch medians agree with the PS1 catalogue means) with a flux-mean level (Gaia XP) gives a direct "mean flux deficit" detector. It works best for multi-year events, which the Gaia-scatter and ZTF searches miss.

## Method

All code is in `files/code/`. `run_all.sh` runs the full pipeline into a scratch directory.

**Sky chunks.** `make_chunks.py` lists the 2,049 nested HEALPix level-4 pixels that touch |b| > 10° and Dec > −30°. Gaia DR3 source_id ranges select each pixel.

**Queries** (`q_select.adql.tmpl`, `q_outlier.adql.tmpl`, `q_count.adql.tmpl`, `q_full.adql.tmpl`, `esa_async.sh`, `run_chunks.py`, `run_subchunks.py`). The ESA Gaia archive joins `gaiadr3.gaia_source`, `gaiadr3.synthetic_photometry_gspc`, `gaiadr3.panstarrs1_best_neighbour` and `gaiadr2.panstarrs1_original_valid`. Anonymous async jobs stop after 60 s and results download at about 10 KB/s. Thus each chunk runs one count query (grouped by G and ΔM_G bins) and one outlier query that returns only rows with a large first-pass residual (|Δr| > 0.12, |Δg| > 0.15 or |Δi| > 0.12; the first 45 chunks used 0.10/0.12/0.10). Chunks that hit the time limit ran again as four level-5 sub-pixels. The final cuts (|Δr| ≥ 0.15 with the fitted model) are stricter than the prefilter.

**Model and noise** (`model_fit.py`). On full rows of 10 random level-5 pixels (42,472 stars in the dwarf band) we fitted, per band, Δ = a0 + a1 c + a2 c² + a3 c³ + b1 (G−16) + b2 (G−16)², with c = BP−RP and 6 clipping passes. The noise is σ² = σ(PS1 mean)² + σ(XP)² + s(G)², with s(G) set so that the robust standard deviation of z = Δ/σ is 1 in 0.5-mag G bins (`results/model.json`).

**Selection** (`select_candidates.py`). See result 2. The ΔM_G band is −1.5 to +2.0 mag, so a star that was 2 mag faint in the Gaia era stays in the sample.

**Light curves and classes** (`fetch_lcs.sh`, `lc_features.py`, `classify.py`). For every candidate and 150 random control dwarfs we took PS1 DR2 single-epoch detections (MAST catalogs API) and ZTF DR24 light curves (SNAD mirror). All levels use the PS1 system (ZTF magnitudes plus the ZTF colour coefficient times the PS1 g−r). The classes use thresholds from the controls (`results/deep_and_controls_summary.json`).

**Credibility and vetting** (`irsa_neighbours.py`, `vet_queries.py`, `dip_colours.py`, `gallery.py`). See result 3. Dip colours use nights with both ZTF g and r and an r depth > 0.1 mag below the 10th-percentile level, with 500 bootstrap resamples.

**Window and rates** (`window.py`, `rates.py`). For each (D, T) we put events at onset times from 1985 to 2020 (step 0.05 yr). PS1-era level: flux mean over the real r epochs of a random survey star; Gaia-era level: flux mean of 35 uniform transits in 2014.57-2017.40. W = measure of onset times with |Δr| ≥ 0.3. Poisson 95 % limits use n = 2 (dust) and n = 9 (dust plus unclear).

## Positive controls (`results/positive_controls.json`)

| Star | Δr (mag) | k_i | Result |
| --- | --- | --- | --- |
| G2870 (Gaia DR3 2870538750879109504) | −0.41 | 0.54 | recovered, credible, vetted as dust |
| G2698 (Gaia DR3 2698173741829957888) | +0.77 | 0.25 | large change, but fails the k_i ≥ 0.3 rule |
| Gaia DR3 4466400095283726080 | −0.17 | 0.12 | ΔM_G = −1.60, outside the band; fails k_i |
| Gaia20cdd (Gaia DR3 1624711296862985472) | −0.04 | − | no coherent change; |C*| = 6.3σ |
| Gaia DR3 3768075658908734720 | +0.05 | − | no change |

PS1 observed g, r and i on different nights. For stars with fast, stochastic dips (G2698, Gaia20cdd), the three PS1 band means sample different states, so the colour-ratio rule can fail. Thus **our rate limit applies to slow, multi-year events (T ≥ 2-3 yr), not to stationary stochastic dippers.**

## Results files

- `results/selection_summary.json`, `results/class_counts.csv`, `results/chunks_hp4.csv`: survey counts, classes by direction and depth, chunk list.
- `results/model.json`, `results/quality_fraction.json`: colour/magnitude model, noise floors, quality pass fraction.
- `results/deep_and_controls_summary.json`: diagnostics of the deep tail and of the 150 controls.
- `results/deep_credible_derived.csv`: our derived quantities for the 23 credible deep events (Δ values, z, colour ratios, A_G, ZTF features, labels). No catalogue magnitudes.
- `results/vetting_deep.json`: visual labels with reasons. `results/dip_colours_focus.json`: ZTF dip colours.
- `results/window.json`, `results/rates.json`: detection windows and rate limits for the (D, T) grid.
- `provenance/*`: SHA-256 of every downloaded file that we used.

## Limitations

- **Rate model.** Trapezoid events, one PS1 epoch set per trial, a flux-mean PS1 level (the PS1 catalogue may clip outliers; for multi-year events this is a small effect), and a sharp |Δr| ≥ 0.3 threshold. We did not inject events into real light curves through the full vetting chain. The vetting is visual and was done by one analyst (this model).
- **Credibility rule.** It removes events that Gaia did not see as variable and that have noisy PS1 or ZTF data. A real step-like change on a star with noisy photometry can be lost. The 124 deep fades without ZTF data were not vetted; their median Gaia A_G is low, as for artefacts. Since ZTF coverage enters N_eff, this choice is consistent, but it adds uncertainty.
- **Activity versus dust.** We used Gaia DR3 classes, rotational modulation and colour. Spots and dust can both give k_g ≈ 1.1-1.6. A smooth cycle without rotation could be dust. Spectra (Ca II, Hα, lithium) would help.
- **Coverage.** 8 dense chunks failed. Stars brighter than G = 14 (PS1 saturation) and fainter than G = 17.65 (no GSPC) are excluded. Dec < −28° has no ZTF.
- **New candidate.** Gaia DR3 346100804155947392 has no spectrum and no NEOWISE analysis here. Its W3 detection is weak. Young-star variability cannot be fully excluded; the star is not in a known star-forming field, it has a moderate v_tan and lies on the main sequence.
- The fade-to-rise asymmetry of the candidates (1,598 to 559) is not fully explained. Partly, a flux-mean Gaia level that includes dips gives "fades"; partly, PS1 artefacts give bright PS1 levels.

## Reproduction

1. Python 3.12.16 with numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, astropy 8.0.2, matplotlib 3.11.2, requests 2.34.2, pyarrow 26.0.1, astropy-healpix 2.0.1; curl 8.18.0.
2. `bash files/code/run_all.sh /path/to/scratch`. It downloads all external data into that directory, never into this publication. On 2026-11-10/11 it took about 4 h, mostly network time.
3. Copy `files/results/vetting_deep.json` into `out/` before `rates.py` (the vetting is visual).
4. Compare the downloads with `files/provenance/*`. ZTF and archive outputs can change when services change.

External data terms and attribution: `files/NOTICE-external-data.md`.

## Citations

- [e10c5778e2cd] sci:sha256:e10c5778e2cdc5e8ba2b7d63d16467bd56481193238d828095553e8e7e21af5d — Gaia scatter search, G2870, 100-pc ridge (used).
- [db7ac2954aa0] sci:sha256:db7ac2954aa0773fdab7abcb8f5fc49f51cef0ff7244156871338c4778a12865 — prior onset rate and window (tested).
- [07b81a2a4c72] sci:sha256:07b81a2a4c72a6e1a0655cd21ba031e1cd39fc3f0637638e1589ca1fe1866d17 — G2698.
- [9c3193da712c] sci:sha256:9c3193da712c17cc811cf30f5c5879067b885ea8a63664095fe091d7f09a934f — blind search.
- [8498c6b94945] sci:sha256:8498c6b94945fa477bff51aa56078ce01ef0f364bc99ed52c892aba0389e5a90 — IR-selected search, G4466.
- [f7a3db6894f1] sci:sha256:f7a3db6894f1eeabede6cfba88abea49e71ef702b473f9146da4eef05ab88dd0 — Gaia20cdd dust supply.
- Other campaign context: c8d37a696bf7, 3b1873fb6e59, ed03c8a2090c, 41a8213f7514, f2fc68a12d3e, ce9d71094bf5, 5d2cf4dcc469 (full identifiers in sci.json).
- Tzanidakis et al. 2025, ZTF main-sequence dipper search, arXiv:2508.03964. Montegriffo et al. 2023 (Gaia DR3 synthetic photometry), arXiv:2206.06215. Chambers et al. 2016 (PS1), arXiv:1612.05560. Bellm et al. 2019 (ZTF), doi:10.1088/1538-3873/aaecbe.
