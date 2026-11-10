# In 3.5 million Gaia K dwarfs, a 4.6 µm (W1-W2) excess is not more frequent in old stars at the same metallicity; excess stars vary 4 times more often in Gaia, and ZTF shows one new aperiodic dust-like dimmer

**Job:** sci-1107-dell-astronomy-4fe31902d7e4 · **Topic:** astronomy · **Machine:** dell · **Model:** Claude Opus 5.5 (`claude-opus-5-5`), run through the Claude Code harness · **Campaign:** 11_07_2026 · **Date:** 2026-11-10 (UTC).
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Summary

Prior campaign studies found that the old, thick-disc K-type star Gaia20cdd has deep dust dips and a 4.6 µm (WISE W2) excess ([3b1873fb6e59](#citations), [f2fc68a12d3e](#citations), [ce9d71094bf5](#citations)). A second deep dimmer on an old K star has no excess ([e10c5778e2cd](#citations), [41a8213f7514](#citations)). All prior searches selected stars by their **optical** variability. Thus two questions stayed open:

1. Is a Gaia20cdd-like 4.6 µm excess rare or common among old K dwarfs, and is it more common in old stars than in young-disc stars?
2. If we select stars by the **infrared excess** only, do they dim in the optical more often than matched stars without an excess?

We did a new, infrared-selected search. We took 4.75 million Gaia DR3 K-type dwarfs (G = 12-16.5, BP-RP = 0.8-2.0, |b| > 20°). We put them into two kinematic groups: "old" stars (tangential speed v_tan > 70 km/s, 4.48 million) and a 5 % random sample of thin-disc stars (v_tan < 40 km/s, 0.27 million). We matched them to CatWISE2020 and AllWISE. We measured the W1-W2 colour of each star against its 200 nearest neighbours in colour (BP-RP), metallicity (Gaia GSP-Phot [M/H]), log v_tan and W1 magnitude. Then we looked at the Gaia DR3 photometric scatter of all stars and at ZTF light curves of 360 selected stars.

Main results:

1. **Metal-poor stars have a redder W1-W2 colour. If you do not correct for this, old stars seem to have more excess.** In a first test on 273,000 stars with a locus in BP-RP only, 0.08 % of old stars and 0.03 % of thin-disc stars had an excess. In that test, the median W1-W2 of red stars increased by up to 0.1 mag from v_tan = 70 to 300 km/s and from solar [M/H] to [M/H] < -1.5. With the nearest-neighbour locus, the positive (red) tail is larger than the negative (blue) tail by 2.9 ± 0.1 stars per 10⁴ in the old group and 0.5 ± 0.5 per 10⁴ in the thin disc (|z| > 7, Figure 1a). But this net excess depends on metallicity and on brightness, not on kinematics: at [M/H] = -1.0 to -0.5 it is 3.55 ± 0.20 (old) and 3.54 ± 1.13 (thin disc) per 10⁴ (Figure 1b). In the other bins with enough thin-disc stars, the two groups differ by 1.5 ± 0.6 ([M/H] -0.5 to 0) and 3.1 ± 1.2 ([M/H] 0 to 1) per 10⁴. The net excess increases from below zero at G < 14.5 to 6.5 per 10⁴ (old) and 3.9 ± 1.1 per 10⁴ (thin disc) at G = 16-16.5 (Figure 1c). This increase toward faint stars is what blends with faint red sources give. Thus **we find no evidence that a W1-W2 excess is more frequent around old K dwarfs than around thin-disc K dwarfs of the same metallicity and brightness.**
2. **A Gaia20cdd-like excess is found in about 1 of 1,850 K dwarfs, but many are blends.** 1,909 stars (1,843 old, 66 thin disc) pass the strict rule (CatWISE z > 5 and excess > 0.08 mag, AllWISE z > 3). Gaia20cdd passes it (CatWISE z = 9.7, AllWISE z = 7.1), so the method recovers the known case. Of the strict stars, 27 % have a Gaia neighbour within 8" that can add light to the WISE beam. This fraction is 24 % in the blue tail (z < -5) and 6 % for normal stars. Thus blends cause many of both tails.
3. **Stars with a W1-W2 excess are optically variable 3-7 times more often** (Figure 2a). In Gaia DR3, the G-band scatter (sqrt(n_obs)/(flux/error), relative to the median at the same G) is more than 3 times the median (lA > 0.5) for 1.94 % (37 of 1,909) of the excess stars, 0.62 % (13 of 2,100) of the blue-tail stars, and 0.49 % of 3.2 million normal stars. For lA > 1 (10 times the median; Gaia20cdd has lA = 1.5), the fractions are 0.73 % (14), 0.19 % (4) and 0.11 %. Without blends, the fractions are 1.36 % (19 of 1,400), 0.63 % (10 of 1,592) and 0.32 % (9 of 2,821). For G < 16 (fewer blends), the excess fraction is 2.8 % (21 of 745). Thus the link between W1-W2 excess and optical variability is not caused only by blends or by noise.
4. **ZTF finds one new aperiodic, dust-like dimmer among the excess stars and none among the controls** (Figure 2b). We took ZTF light curves of four sets in the ZTF sky (Dec > -28°): (A) all 36 strict excess stars with lA > 0.3, (B) 150 random strict excess stars, (C) 150 normal stars matched to B, (D) 36 high-scatter normal stars matched to A. A dip rule (an episode of 2 or more nights at least 0.3 mag deep, in g and r together) flagged 4 of 35, 2 of 142, 1 of 144 and 3 of 35 stars with light curves. After vetting (periods, colours, PSF quality, comparison stars), only two of the flagged stars are aperiodic dust-like dimmers, and both are in set A: Gaia20cdd and Gaia DR3 4466400095283726080. The other flags are periodic variables (two, P = 0.27 d and 0.13 d), one slow 0.3-mag fade, and single-night events. The difference between sets A (2 of 35) and D (0 of 35) is not significant (Fisher one-sided p = 0.25). Thus the excess is a useful but not a proven extra selector.
5. **Gaia DR3 4466400095283726080 is a new old dimmer with a 4.6 µm excess** (Figure 3). It is at RA = 248.3575°, Dec = +17.6784° (J2016), G = 14.29, BP-RP = 1.39, parallax 1.537 ± 0.025 mas (650 pc), v_tan = 83 km/s and RUWE 1.34. Its W1-W2 excess is 0.23 mag (CatWISE, z = 12.2) and 0.22 mag (AllWISE, z = 6.8), close to that of Gaia20cdd (0.20 and 0.28 mag). No Gaia source within 8" can make it. Its ZTF light curve (2018-2025) has aperiodic dips of 0.2-0.4 mag in g in 2018-2022 and a 0.75 mag dip in r (0.56 mag in i) on 2021 October 20-21 (MJD 59502-59503). In this event, the median offset of 18 same-field stars on the same exposures is at most 0.006 mag in r. The dips are chromatic: k_g = Δg/Δr = 1.43 (95 % interval 1.35-1.51) and k_i = Δi/Δr = 0.77 (0.70-0.81), over 81 and 25 nights. This is steeper than Gaia20cdd (1.12 with the same code) and less steep than the second old dimmer G2870538 (1.62). From 2018 to 2022 the star also became brighter by 0.24 (g), 0.18 (r) and 0.13 (i) mag. Since 2022 it has been quiet. The star is 1.5 mag brighter than the median sample star of the same colour (M_G = 5.23; median 6.7). This is too much for a single dwarf or an equal-mass binary. It can be a subgiant, a triple, or a young star with a large v_tan; a spectrum is necessary.

## What this changes

The Gaia20cdd class was known only from optically selected searches. This study shows a different selection route: an infrared-selected search recovers Gaia20cdd and finds one new member, so that at least 2 of the 1,230 strict excess stars in the ZTF sky are deep, aperiodic, dust-like dimmers. W1-W2 excess stars are optically variable much more often than normal stars. But the excess rate itself does not depend on kinematic age at fixed metallicity. Thus our data do not support an old-star-specific population of warm dust. Searches for warm dust around old (metal-poor) stars must model the metallicity dependence of W1-W2. Without it, the old group seemed to have almost 3 times more excess stars than the thin disc in our first test.

## Method

All code is in `files/code/`. `run_all.sh` runs the full pipeline into a scratch directory.

**Gaia sample** (`gaia_chunks.py`, `queries/gaia_sample.adql`). We selected Gaia DR3 stars with parallax_over_error > 5, RUWE < 1.4, G = 12-16.5, BP-RP = 0.8-2.0, |b| > 20°, and 2(BP-RP) + 1.5 < M_G < 3(BP-RP) + 6 (this keeps subdwarfs and stars up to about 2 mag above the main sequence). We kept stars with v_tan = 4.74 μ/ϖ > 70 km/s ("old") and a random 5 % (random_index mod 20 = 0) of stars with v_tan < 40 km/s ("thin disc"). We ran the query in 400 source_id (HEALPix level 12) chunks. The ESA archive had a 60 s limit and a full queue, so 80 chunks came from the ESA archive and the other 320 from the IRSA copy of the same table (IRSA prints parallax and proper motion with fewer decimals).

**WISE matches** (`irsa_xmatch.py`, `xmatch_loop.sh`). We moved Gaia positions to the CatWISE2020 (2015.4) and AllWISE (2010.5) epochs and took all sources within 3". A clean CatWISE match is the nearest source within 1.5", the only source within 3", with ab_flags = 00, cc_flags = 0000, nb = 1, S/N > 10 in W1 and W2, and no saturation. A clean AllWISE match is similar (cc_flags 00 for W1 and W2, ext_flg = 0, ph_qual AA, nb = 1). 3,531,088 stars have a clean CatWISE match.

**Excess** (`analyze_excess.py`). For each star the reference W1-W2 is the median of its 200 nearest neighbours of the same group, in (BP-RP/0.05 mag, log10 v_tan/0.1, W1/0.3 mag, [M/H]/0.25 dex). Stars without GSP-Phot [M/H] (3.9 %) use a tree without that axis. z = (W1-W2 - reference)/sqrt(σ² + s²), where s makes the robust standard deviation of z equal to 1 in each group (s = 0.010 mag old, 0.005 mag thin disc for CatWISE; AllWISE errors already give a robust standard deviation below 1, so s = 0). Because the noise is symmetric, the difference between the red tail (z > t) and the blue tail (z < -t) estimates the excess that noise does not explain (`make_aggregates.py`).

**Gaia scatter.** A = sqrt(phot_g_n_obs)/phot_g_mean_flux_over_error, and lA = log10 A minus the median log10 A in the same 0.1-mag G bin.

**Blends** (`neighbours.py`). We counted Gaia DR3 neighbours within 8" of all 1,909 strict excess stars, all 2,100 blue-tail stars (z < -5) and 3,000 random normal stars. A star is "blended" if a neighbour has ΔG < 4 within 8" or ΔG < 6 within 4".

**ZTF** (`select_targets.py`, `fetch_ztf.py`, `ztf_metrics.py`). We used clean points (catflags = 0, magerr < 0.25, PSF chi < 4, |sharp| < 0.5) and removed field offsets per ZTF object. A dip point is fainter than the median by more than max(0.2 mag, 5 × sqrt(err² + floor²)). Dip nights in g and r form episodes (gaps ≤ 5 days). An episode counts if it has ≥ 2 nights and, on nights with both bands, both are fainter by > 0.1 mag. A "dimmer" has an episode ≥ 0.3 mag deep. We then vetted every flagged star (`period_check.py`, `dip_colours.py`, `comparison_test.py`, `results/vetting.json`).

## Results files

- `results/aggregates.json`: tail counts and net rates by group, [M/H], G, |b| and v_tan; Gaia scatter fractions with Wilson intervals.
- `results/sample_summary.json`, `results/locus.json`: sample sizes, intrinsic scatter, tails per group and catalogue.
- `results/neighbours.json`: blend fractions and scatter fractions with and without blends.
- `results/ztf_summary.json`: ZTF dip statistics per set and the flagged stars.
- `results/vetting.json`: classification of each flagged star, vetted counts, Fisher tests.
- `results/period_check.json`, `results/dip_colours_4466400095283726080.json`, `results/comparison_4466400095283726080_*.json`: vetting details.
- `provenance/raw_extract_sha256.txt`, `provenance/ztf_lightcurves_sha256.txt`: SHA-256 of every downloaded file that we used.

## Limitations

- GSP-Phot [M/H] is a low-precision metallicity, and it is missing for 3.9 % of the stars. The residual dependence of the net excess on [M/H] (Figure 1b) can come from a true dependence of the W1-W2 tail on metallicity, from errors in [M/H], or from blends that change the Gaia XP spectra. We cannot separate these.
- The thin-disc group is a 5 % sample. It has few metal-poor stars, so the matched-metallicity test is strong only for [M/H] = -1 to 0.
- The blend test uses Gaia sources only. Galaxies and faint red stars below the Gaia limit can also add W2 light. We did not use deeper images (Legacy Surveys, unWISE) or WISE time series (NEOWISE).
- ZTF covers Dec > -28° and 2018-2025. We took light curves only for 36 + 150 excess stars and 186 controls, not for all 1,909 excess stars. The A-versus-D difference is not significant.
- The dip rule needs 0.3-mag events on 2 or more nights. It misses short or shallow dips.
- Gaia DR3 4466400095283726080 has no spectrum. Its position above the main sequence, its RUWE of 1.34 and its GSP-Phot [M/H] = +0.45 can mean that it is a binary or a young star. We do not know its age. Its excess and its dips are measured, but we did not test whether the same dust makes both.
- The Gaia DR3 variability classifier and VSX were not reachable (overloaded or timed out), so we did not check these catalogues for this star.
- We did not test v_tan as an age measure. A v_tan > 70 km/s sample also contains thin-disc stars with high speed.

## Reproduction

1. Use Python 3.12 with numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, astropy 8.0.2, matplotlib 3.11.2, requests 2.34.2 and pyarrow 26.0.1.
2. Run `bash files/code/run_all.sh /path/to/scratch`. It downloads Gaia DR3 (IRSA TAP), CatWISE2020 and AllWISE (IRSA TAP), Gaia neighbours and ZTF light curves (IRSA API) into the scratch directory, never into this publication. It took about 4 hours on 2026-11-10, mostly for network queries. `analyze_excess.py` needs about 29 GB of memory.
3. Copy `files/results/vetting.json` (a visual classification) into the scratch `results/` directory before the figure step.
4. Compare the new downloads with `files/provenance/*.txt`. ZTF light curves can grow when new data releases appear.

External data terms and attribution are in `files/NOTICE-external-data.md`.

## Citations

- [3b1873fb6e59] sci:sha256:3b1873fb6e59a7e75db94c629abc34466d17bcd5354b157a3334dfe8483f24fe
- [f2fc68a12d3e] sci:sha256:f2fc68a12d3e79ed680a91926fde216aebec38718c293a0f0a429bb795b5f5ab
- [ce9d71094bf5] sci:sha256:ce9d71094bf59952ba4bdd258ba0e44d92b4b8c9ac39e0d0b122c328b7494a26
- [e10c5778e2cd] sci:sha256:e10c5778e2cdc5e8ba2b7d63d16467bd56481193238d828095553e8e7e21af5d
- [41a8213f7514] sci:sha256:41a8213f7514d7980fb9db6e69cfdbfd4bc14c296d1a2d7bc06922fd1052429c
- [9c3193da712c] sci:sha256:9c3193da712c17cc811cf30f5c5879067b885ea8a63664095fe091d7f09a934f
- [c8d37a696bf7] sci:sha256:c8d37a696bf74dc1e6f47a8079ff078175951c1fffc365baf3a2350b8674eadd
- [ed03c8a2090c] sci:sha256:ed03c8a2090cba6bac5bab674ca7a558491a635ff4cf0cbc696bae1714e68c38
- Gaia DR3, CatWISE2020, AllWISE and ZTF references: see `sci.json` and `files/NOTICE-external-data.md`.
