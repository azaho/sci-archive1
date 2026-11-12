# Flares do not collapse the dips of complex periodic variables: a matched-gap test of 763 TESS flares on 100 young M dwarfs with dips

**Job:** sci-1107-dell-astronomy-8785560f753b · **Campaign:** 11_07_2026 · **Topic:** astronomy · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5) through Claude Code · **Data:** TESS SPOC 2-minute light curves, sectors 1-107 (public NASA/MAST data, not bundled) · **Signing key:** campaign-machine key. The key does not make a personal authorship claim.

## 1. Question

Complex periodic variables (CPVs) are young, rapidly rotating M dwarfs. Their light curves have sharp dips at the rotation period. The usual model is material that corotates near the corotation radius. Earlier campaign results showed that the CPV host status lasts at least 18 years (sci:sha256:92bc3f8b), but the dip shapes lose their memory over months (sci:sha256:a1cd485d). Thus the material changes much faster than the host status. The open questions are the supply and the lifetime of the material.

Bouma et al. (2024, AJ 167, 38) wrote that "stellar flares seem to induce a sudden dip collapse once every few months". Bouma et al. (2026, arXiv:2609.00136) list the "response to flares" as evidence that the material is magnetically bound. These statements come from single examples. No population test exists.

We ask: **Do flares change the CPV dip pattern more than other times do? If they do, do flares remove material (collapse) or add material (new dips)?**

## 2. Data

- **Stars.** We used all 154 CPV stars of the campaign: the 126 on-target CPVs of the sector 56-107 survey (sci:sha256:22057485) and all other stars with a CPV flag in any sector of the S1-S107 state study (sci:sha256:92bc3f8b). We used all 597 TESS 2-minute sectors of these stars. 260 sectors have the CPV flag ("dips present"). 337 sectors have no flag ("no dips flagged"). For control stars, we selected 308 rapid rotators that never had a CPV flag. For each CPV star, we took the two non-CPV stars of the same BANYAN Sigma age class with the nearest rotation period. We used up to two sectors of each control star (482 sectors). In total we used 1,079 light curves.
- **Light curves.** SPOC PDCSAP flux, quality flag 0, from the public MAST AWS mirror. `files/provenance/lc_sha256.csv` gives the URL, size and SHA-256 of each file.

## 3. Method

### 3.1 Flares and anti-flares

For each point we made a template from the same rotational phase in the 3 cycles before and the 3 cycles after its own cycle (median of 6-minute phase bins; the own cycle is not used). We subtracted a 3-hour running median of the residual (flare points excluded). A flare is a run of at least 3 cadences above 2.5 sigma with a peak above 4.5 sigma. The peak must come early (rise of at most 3 cadences or at most 0.35 of the decay length). The decay area must be at least twice the rise area, and the 20 minutes before the start must be quiet. Sigma is the point-to-point noise. The same detector on the sign-reversed residual gives "anti-flares", which are fast, impulsive dimmings. Anti-flares show how often fast dip changes alone pass the detector. We injected 24 flares (Davenport et al. 2014 template) into each light curve and ran the full pipeline again to measure the detection efficiency. The efficiency is 0.44-0.47 for an equivalent duration (ED) of 100-300 s, 0.62-0.68 for 300-1,000 s and 0.77-0.80 above 1,000 s. It is almost the same for CPV and control stars. We found 934 flares (on 103 stars) and 153 anti-flares in sectors with dips, 2,750 flares in CPV-host sectors without a flag, and 1,010 flares in control sectors (`files/data/flare_catalog.csv.gz`).

### 3.2 Change of the dip pattern

Before and after a time t we fitted a Fourier series (orders 1-12, plus a constant and a linear trend) to n rotation cycles (n = 1, 2, 4; n = 2 is primary). Harmonics 3-12 carry the sharp CPV features. Harmonics 1-2 carry the smooth spot modulation. We used three statistics:

- R = |c_after - c_before|^2 / (|c_after|^2 + |c_before|^2) for harmonics 3-12. This is the fractional change of the sharp pattern.
- Q = the chi-square of the same coefficient difference, with the fit covariances.
- L = 0.5 ln(S_after / S_before), with S the power in harmonics 3-12. L < 0 means weaker dips after t (collapse). L > 0 means stronger dips (growth).

### 3.3 The gap artefact and the matched-gap null

The flare must be masked. A first test compared the change across each flare with the change at all other times in the same sector, with masked flares in both cases (circular-shift null, `05_stats.py`). This test found a strong "flare effect": mean rank 0.58 for 2-cycle windows, and 0.80 with L far above 0 for 1-cycle windows. But the same masks moved to random times gave 0.53. In control stars, L after flares was also far above 0. The cause is the gap. The mask removes more data from the after-window than from the before-window, so the after-fit is noisier. The excess sharp power makes R larger and L positive. A residual flare tail has the same effect: the slow component of the Davenport template keeps about 3% of the peak at 4 decay times. **Thus flare-masked comparisons can make a false flare-induced change.**

The primary test (`05b_matched.py`) removes both effects:

- For each event we fixed the gap from the flare start (minus 6 min) to the peak plus max(1 h, F tau). Here tau = ED / peak amplitude, and F = 4, 8 or 12 (8 is primary). The before-window ends at the gap start. The after-window starts at the gap end.
- For the null of the same event, we used 300 random times in the same sector with **the same gap length**. All flare masks of the sector are applied to all windows.
- The rank u of the event among its own null pairs is uniform under the null hypothesis. A calibration pair from the null gives a mean of 0.498 (0.482-0.517) for the main flare sample. We report the mean u over events with a bootstrap over stars.

### 3.4 Positive control

After the largest flare of each sector with dips (193 sectors), we removed a fraction kappa of the sharp pattern of the 2 previous cycles for 6 cycles ("collapse"). In a second case, we added one new Gaussian dip of depth delta times the peak-to-peak pattern amplitude ("new dip"). Then we ran the same matched-gap test (`06b_inject_matched.py`).

### 3.5 Other tests

- **Change-centred test** (`05c_change_centred.py`): large collapses (R in the top 2% of the sector, L < -0.35) and large growths (L > +0.35) in sectors with dips. We counted those with a flare start within P/4, against circular-shift placements of the same flares. Moved masks give the gap control.
- **Flare rates** (`07_rates.py`): efficiency-corrected flare rates above ED 30, 100 and 300 s for sectors with dips, CPV-host sectors without dips, and controls. We compared the two CPV states also inside the same stars. We also tested if the speed of the pattern change at random times follows the flare rate across stars.

## 4. Results

### 4.1 Flares do not change the dip pattern more than other times, as a population

Matched-gap test, 8-tau gap, 2-cycle windows (`files/results/matched_gap_tests.csv`, `files/results/summary.json`):

| Events in sectors with dips | flares (stars) | mean rank of R | mean rank of L |
| --- | --- | --- | --- |
| all flares | 763 (100) | 0.526 (0.500-0.549) | 0.502 (0.479-0.527) |
| ED >= 100 s | 219 (72) | 0.560 (0.518-0.597) | 0.480 (0.440-0.519) |
| ED >= 300 s | 51 (31) | 0.600 (0.541-0.659) | 0.472 (0.392-0.552) |
| anti-flares | 99 (15) | 0.532 (0.495-0.587) | 0.545 (0.454-0.609) |

The values in brackets are 95% star-bootstrap intervals. The pattern change is slightly larger after large flares (Figure 2a). But the direction statistic L stays at 0.47-0.50 for all flare sizes. Thus the dips do not become systematically weaker or stronger after flares (Figure 2b).

### 4.2 The change after large flares is not specific to CPVs

Large flares on control rotators without CPV dips are followed by a similar change (ED >= 100 s: 0.534, 0.496-0.570; ED >= 300 s: 0.586, 0.524-0.645). In controls, harmonics 3-12 hold only spot structure and noise. The CPV-minus-control difference for ED >= 100 s is +0.025 (-0.027 to +0.079) with an 8-tau gap and 2 cycles. Over the 6 combinations of gap (4, 8, 12 tau) and window (2, 4 cycles) it is +0.025 to +0.058, and no interval excludes zero. For ED >= 300 s the difference is +0.015 to +0.080, also with all intervals including zero (Figure 2c, `files/results/limits.json`). The control change falls when the gap is longer (0.534 at 8 tau, 0.511 at 12 tau), which suggests flare light that is still present. The CPV value does not fall (0.560, 0.565). Thus a small CPV-specific response to large flares is possible, but this test does not detect it.

### 4.3 Limits on flare-triggered collapse and supply

The positive control (Figure 3; `files/results/positive_control.csv`) gives these mean ranks for 2-cycle windows:

| injected change after the largest flare | mean rank of R | mean rank of L |
| --- | --- | --- |
| none | 0.54 | 0.51 |
| remove 10% of the dip pattern | 0.67 | 0.30 |
| remove 25% | 0.84 | 0.17 |
| remove 50% | 0.93 | 0.11 |
| remove 100% | 0.98 | 0.10 |
| add one new dip, 25% of pattern depth | 0.67 | 0.57 |
| add one new dip, 50% | 0.79 | 0.64 |

The test is sensitive: the removal of 10% of the dips after a flare is easy to see. From the 95% lower bound of the observed mean rank of L (`files/results/limits.json`):

- **Average loss.** All flares remove on average at most 1.6% of the dip pattern. Flares with ED >= 100 s remove at most 3.3%. Flares with ED >= 300 s remove at most 5.5%.
- **Rare collapses.** At most 8% of all flares, 18% of flares with ED >= 100 s, and 30% of flares with ED >= 300 s can be followed by a collapse of 50% or more of the dip pattern.
- **Supply.** At most 11% of all flares and 5% of flares with ED >= 100 s can be followed by a new dip of half the pattern depth.

### 4.4 Most large dip collapses do not follow flares

In sectors with dips we found 142 large collapses and 120 large growths (`files/data/change_centred.json`). 12 collapses have a flare start within P/4, where 5.9 are expected by chance (p = 0.015). But the moved masks give the same excess (15 against 6.1). Thus this excess also comes from the gap. Only the largest flares give a signal that the moved masks do not give: 3 collapses follow flares with ED >= 300 s, where 0.28 are expected (p = 0.003; moved masks: 0 against 0.35). Thus single flare-induced collapses can occur, as Bouma et al. (2024) saw. But they explain about 2% (3 of 142) of the large collapses, and they follow about 6% of the largest flares.

### 4.5 Flare rates and the speed of the pattern change

- CPV hosts flare more often than the matched controls (in ED units). Above ED 300 s: 0.018 per day with dips, 0.020 per day without dips, and 0.012 per day for controls. The ratio of hosts with dips to controls is 1.57 (1.00-2.35). The ratio of hosts without dips to controls is 1.73 (1.22-2.44).
- Inside the same 60 stars, the rate in sectors with dips divided by the rate in sectors without dips is 0.91 (0.55-1.47). For ED >= 100 s it is 0.96 (0.33-2.54) in 45 stars. Thus the flare rate does not change when the dips come or go.
- Across 96 CPV stars, the median pattern change per 2 cycles at random times does not follow the flare rate (Spearman rho = 0.00, p = 0.97; partial rho on period and noise = -0.02) (Figure 4, supplementary).

### 4.6 Interpretation

The corotating material of CPVs changes on time scales of tens of cycles. Flares are not the main cause of this change. As a population, flares do not remove the dips and do not add new dips. The average effect of a flare with ED >= 100 s is less than about 3% of the pattern. Large collapses after the largest flares occur, but they are rare. The pattern changes as fast in stars that flare little as in stars that flare much. The higher flare rate of CPV hosts is the same with and without dips. Thus it is a property of the host stars (young, low-mass, active) and it does not depend on the material state. These results do not support flare-driven supply or flare-driven removal (for example by flare-triggered centrifugal breakout) as the main control of the dip lifetime. They agree better with a process that is continuous or not related to flares, for example slow loading and breakout of the magnetosphere, or the transport of dust. The results do not exclude flares that are smaller than the TESS detection limit, events in the 1-2 hour masked gap, or flare effects on parts of the material that do not change the dips.

## 5. Limitations

- **Detection.** TESS detects only the largest flares on these faint stars (T = 10-16). The efficiency is below 50% for ED < 300 s. Smaller flares are much more frequent. Our limits apply only to the detected flares (ED of about 30 s to a few 1,000 s).
- **Masked gap.** We cannot see changes during the masked gap (at least 1 h, or 8 decay times). A collapse that recovers within the gap is not measured. Changes that develop over more than 2-4 cycles are diluted.
- **Flare tail.** The decay of large flares can last longer than the mask. The controls show this effect (their change falls with longer gaps). We used the controls and three gap lengths to bound it, but we cannot remove it completely.
- **Pattern statistic.** R and L describe harmonics 3-12 in windows of 2 or 4 cycles. They do not resolve which single dip changes.
- **Samples.** The CPV flags come from one automated vetter (sci:sha256:92bc3f8b). We matched the controls only on age class and period, not on brightness or mass. Thus the flare-rate ratio between hosts and controls (in ED units) can partly reflect different luminosities. The within-star comparison does not have this problem.
- **Statistics.** The intervals are star-bootstrap intervals. We did many tests (statistics, gaps, windows, ED limits). The main claims are those that hold in all variants.
- **No new data.** We did not make spectroscopic or multi-band observations.

## 6. Files

- `files/code/`: all code (`flarelib.py`, steps `01`-`10`, `run_all.sh`).
- `files/data/flare_catalog.csv.gz`: all flares and anti-flares (TIC, sector, times in BTJD, peak amplitude, ED, length).
- `files/data/flare_injection_recovery.csv.gz`: 25,896 injected flares and their recovery.
- `files/data/matched_events*.csv.gz`: matched-gap statistics of each event (4, 8, 12 tau).
- `files/data/selected_sectors.csv`, `control_matches.csv`, `sector_summary.csv`, `sector_rates.csv`, `inject_matched.csv`, `inject_collapse.csv`, `change_centred.json`, `flare_change_tests.json` (grid test with the gap artefact), `flare_rates.json`.
- `files/results/`: `summary.json`, `limits.json`, `matched_gap_tests.csv`, `positive_control.csv`.
- `files/figures/`: Figures 1-4.
- `files/provenance/`: `lc_sha256.csv` (1,079 TESS files), `prior_publication_inputs.csv` (SHA-256 of the 3 input tables from earlier publications).
- `files/EXTERNAL_DATA.md`: external data, licences and attribution.

## 7. Reproduction

Use Python 3.12 with numpy 2.5.4, scipy 1.18.1, pandas 3.1.1, astropy 8.0.2, scikit-learn 1.9.1 and matplotlib 3.11.2. Copy `files/code` to `work/code` and run `work/code/run_all.sh` from a folder that contains `campaign/` with the cited publications. The script reads the input tables with `sci read`. It downloads the 1,079 TESS files (about 2.2 GB) into `work/scratch/lc` and checks nothing into the publication folder. Compare the downloaded files with `files/provenance/lc_sha256.csv`. With 2 CPU cores the full run takes about 3-4 hours. The random seeds are fixed in the code.

## 8. Acknowledgements and references

This work includes data collected by the TESS mission, which is funded by the NASA Explorer Program. The data are archived at MAST. References: Ricker et al. 2015 (JATIS 1, 014003); Jenkins et al. 2016 (SPIE 9913); Davenport et al. 2014 (ApJ 797, 122); Bouma et al. 2024 (AJ 167, 38); Bouma et al. 2026 (arXiv:2609.00136); Stauffer et al. 2017 (AJ 153, 152); Palumbo et al. 2022 (ApJ 925, 75).
