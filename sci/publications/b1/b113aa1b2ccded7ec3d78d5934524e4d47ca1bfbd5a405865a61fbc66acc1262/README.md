# Long-serving Breeding Bird Survey observers recorded fewer high-pitched birds; because cold-adapted species sing higher, this drift made 31-77% of the within-observer CTI warming trend (1966-2025)

Job: sci-1107-dell-climate-pollution-biodiversity-584a8134fa04. Topic: climate-pollution-biodiversity. Campaign 11_07_2026. Machine: dell. Model: Claude Opus 5.5 (claude-opus-5-5) as an automated research worker. The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

Earlier campaign work found that the bird Community Temperature Index (CTI) of the North American Breeding Bird Survey (BBS) followed less than 10% of breeding-season warming (sci:sha256:c0a3a9aa...). That study also found two observer signals. The CTI trend was 0.015 C per decade with observer fixed effects and only 0.001 C per decade without them. The CTI also increased by about 0.009 C per 10 years of observer tenure. The cause of these signals was not known.

We tested one specific mechanism:

1. Age-related hearing loss removes high frequencies first.
2. If cold-adapted bird species sing at higher frequencies than warm-adapted species, an observer who serves for a long time detects fewer cold species.
3. Then the CTI of a route increases while the same observer serves, even if the community does not change.
4. A model with route x observer fixed effects measures the CTI trend only from change inside each observer's period. Thus such a model includes all of this drift.

We wrote the plan (files/ANALYSIS_PLAN.md) before we calculated any outcome.

## 2. Data

- BBS 2026 release (1966-2025), USGS and ECCC, doi:10.5066/P144YU3S: States.zip (10-stop counts), Weather.csv (runs and observer numbers), Routes.csv, SpeciesList.csv. We used 130,303 standard runs (RunType 1, RPID 101) on 5,319 routes.
- NOAA GHCN_CAMS monthly 0.5 degree land air temperature (air.mon.mean.nc, copy of 2026-11-05). We used the May-July mean.
- Song frequencies of Sagar et al. (2024, Proc. R. Soc. B, doi:10.1098/rspb.2024.1908), Dryad doi:10.5061/dryad.69p8cz99k (CC0). These are dominant, top and bottom frequencies from more than 140,000 xeno-canto recordings. We used the Nearctic values when the species had 3 or more Nearctic recordings. Otherwise we used the recording-weighted mean over realms.

The exact paths, URLs and SHA-256 hashes are in files/PROVENANCE.md.

## 3. Methods

Species and STI. We used landbirds (we removed water-bird orders), combined forms into species by binomial, and kept 340 species recorded on 50 or more routes. Of these, 323 species had a song frequency. The Species Temperature Index (STI) is the abundance-weighted mean of the 1981-2010 May-July route temperature. We cross-fitted the STI: for each random half of the routes, we calculated it from the other half. The CTI of a run is the mean STI with log(1 + count) weights. CTI_low uses only species below the median dominant frequency (3.97 kHz). CTI_high uses only the species at or above the median. hf_share is the log-weighted share of birds at or above 3.97 kHz.

Test P1 (species). We regressed STI on dominant frequency across species. We also did this with log body mass, and with log mass plus family fixed effects.

Test P2 (observer turnover). On a route, an observer change compares two people at the same place within 1-3 years. We used 5,740 changes on 2,941 routes. Both observers had 2 or more runs, and the gap was 3 years or less. For each change, we subtracted the mean of the outgoing observer's last 3 runs from the mean of the incoming observer's first 3 runs. If detection decreases with tenure, the incoming minus outgoing difference increases with the outgoing observer's tenure. We regressed the differences on outgoing tenure and gap. We used no fixed effects, event-year fixed effects, or BCR x decade fixed effects, with route-clustered errors and a route bootstrap (150 draws). The temperature change between the two windows is a placebo outcome.

Test P3 (species x frequency). For each species in each change, the outcome is log((mean incoming count + 0.5)/(mean outgoing count + 0.5)). We fitted species x decade fixed effects, outgoing tenure, and tenure x standardized dominant frequency (364,788 species-events).

Test P4 (consequence for tracking). We calculated CTI and temperature trends per decade with route x observer fixed effects and with route fixed effects only. The tracking ratio is the CTI trend divided by the temperature trend on the same runs. We used two corrections. (a) Count correction: we multiplied each count by exp(gamma x z_f x tenure), where gamma is the P3 frequency interaction and z_f is the standardized frequency, and calculated the CTI again. (b) Drift subtraction: we subtracted the CTI drift per decade of tenure from P2 from the within-observer trend. The bootstrap repeats all steps of P2-P4 for each draw.

## 4. Results

### 4.1 Cold-adapted species sing higher (P1)

Across 323 species, the STI decreased by 0.57 C per kHz of dominant frequency (SE 0.16, p = 0.0005; Spearman rho = -0.15, p = 0.006). With log body mass, the slope was -0.65 C per kHz (p = 0.0006). Inside families, the slope was -0.35 C per kHz (p = 0.09). Species at or above 3.97 kHz had a mean STI of 17.1 C. Species below it had 18.6 C. Examples: Golden-crowned Kinglet (7.6 kHz), Cape May Warbler (7.9 kHz) and Blackburnian Warbler (7.5 kHz) are cold species. Mourning Dove (1.3 kHz) and Northern Bobwhite (1.8 kHz) are warm species (Figure 1).

### 4.2 Detection of high-pitched birds decreased with tenure (P2, P3)

- The high-frequency share increased at an observer change by 0.075 percentage points per year of outgoing tenure (95% bootstrap CI 0.060 to 0.089; BCR x decade fixed effects 0.074, CI 0.058 to 0.088). After outgoing tenures of 20 years or more, the mean increase was 2.1 percentage points. After tenures of 1-4 years, it was 0.23 points (Figure 3).
- The effect increased steadily with song frequency (Figure 2). The precision-weighted mean count change per year of outgoing tenure was:
  - -0.02% per year below 2 kHz
  - +0.15% per year at 3-4 kHz
  - +0.41% per year at 4-5 kHz
  - +0.86% per year at 5-6 kHz
  - +0.88% per year at 6-7 kHz
  - +1.62% per year above 7 kHz

  The P3 interaction was +0.39% per year per SD of frequency (1.55 kHz) (SE 0.034%, bootstrap CI 0.32% to 0.46%). Across 286 species, the per-species tenure slopes increased with frequency (Spearman 0.55). The link stayed with controls for log mass, log abundance and order (p < 0.0001), in passerines only, and with top frequency.
- The incoming observer also recorded more species after long-tenure observers: +0.06 species per year of outgoing tenure (CI 0.03 to 0.08). Thus there was also a general detection loss.
- An incoming observer who already had a long BBS career recorded a smaller increase of the high-frequency share (-0.035 percentage points per year of incoming career, p < 0.0001). This also agrees with an effect of observer age.
- The high-frequency result was the same in these subsets:
  - East and West of 100 W
  - changes before 2000 and from 2000
  - outgoing observers who left the BBS (65%) and outgoing observers who stayed on other routes
  - incoming windows without the first year of the incoming observer
- Placebo: the May-July temperature change between the windows did not depend on outgoing tenure (0.0015 C per year, CI -0.0009 to 0.0037).

### 4.3 The detection drift increases the CTI (P2)

At an observer change, the CTI decreased by 0.0011 C per year of outgoing tenure without fixed effects (CI -0.0018 to -0.0003). With event-year or BCR x decade fixed effects, it decreased by 0.0019 C per year (CI -0.0025 to -0.0011). The fixed effects remove calendar changes. Mean outgoing tenure was longer in later years, so the estimate without fixed effects is probably too small. After outgoing tenures of 20 years or more, the mean CTI decrease was 0.038 C.

The CTI of low-frequency species had no tenure drift (-0.0006 C per year, CI -0.0014 to 0.0004). The CTI of high-frequency species had a drift of -0.0020 C per year (CI -0.0027 to -0.0011). Thus the drift is a CTI increase of 0.011 to 0.019 C per decade of tenure. This agrees with the 0.009 C per 10 years reported in sci:sha256:c0a3a9aa..., and it gives the mechanism for it.

### 4.4 Consequence for climate tracking (P4)

Temperature increased by 0.274 C per decade on the same runs (route x observer fixed effects). Our uncorrected within-observer CTI trend (0.024-0.027 C per decade) is larger than the 0.015 C per decade of sci:sha256:c0a3a9aa.... The species set, the period (to 2025), the STI weights and the error model are different. Tracking ratios (route bootstrap 95% CI, Figure 4):

| CTI and model | CTI trend (C per decade) | Tracking ratio |
| --- | --- | --- |
| Species with frequency, route x observer FE | 0.024 | 0.089 (0.076 to 0.103) |
| Same, frequency-corrected counts | 0.017 | 0.061 (0.050 to 0.075) |
| Same, minus turnover drift (no FE) | 0.013 | 0.048 (0.023 to 0.082) |
| Same, minus turnover drift (BCR x decade FE) | 0.006 | 0.020 (-0.000 to 0.052) |
| Species with frequency, route FE only | 0.001 | 0.005 (-0.004 to 0.015) |
| Low-frequency species, route x observer FE | 0.031 | 0.111 (0.094 to 0.131) |
| Low-frequency species, route FE only | 0.024 | 0.091 (0.078 to 0.102) |
| High-frequency species, route x observer FE | 0.002 | 0.006 (-0.011 to 0.026) |
| High-frequency species, route FE only | -0.022 | -0.084 (-0.097 to -0.068) |

The corrections reduced the within-observer CTI trend by 31% (count correction), 46% (drift without FE) and 77% (drift with BCR x decade FE). The count correction uses only a linear frequency term, so it probably removes too little. The drift subtraction includes all species-specific drifts that correlate with STI, not only hearing.

The low-frequency CTI has no detection drift. For this CTI, the two models agreed closely (0.111 and 0.091). These species tracked about 9-11% of warming. For the high-frequency species, the two models did not agree. Within observers their CTI did not change. Across observer changes it decreased. New observers recorded more cold high-pitched birds than the observers they replaced (intercept +0.22 percentage points at zero tenure). Thus the high-frequency CTI mostly shows observer effects, in both directions.

## 5. Interpretation

1. Part of the observer artefact found in earlier campaign work has a physical cause that we can measure. As observers serve longer, they record fewer high-pitched birds. The loss increases steadily with song frequency, as hearing loss does. Because cold-adapted species sing higher, this loss makes the CTI increase.
2. Route x observer fixed effects do not remove this artefact. They put the artefact into the trend. At least 31% of the within-observer CTI trend, and possibly 77%, came from this drift.
3. Models without observer effects have the opposite error, because observer replacement brings in better detection of high-pitched birds. Neither standard model measures the true CTI change of all species.
4. A CTI from species that sing below about 4 kHz has no detectable drift and gives the same answer in both models. This CTI followed about 10% of May-July warming. Thus the main conclusion of the earlier work stays: bird communities followed only a small part of warming. But the all-species estimates of 6-10% are not strong evidence of a climate response. With a correction for the drift, they become 2-6%.
5. For indicator programmes: report a CTI without high-frequency species, or model detection by song frequency x observer tenure. Observer age data would make this better.

## 6. Limitations

- We do not know observer ages. Tenure and career length are only proxies. Other tenure effects can also cause the general detection loss (+0.06 species per year), for example less effort, a changed route habitat, or less motivation. The frequency gradient and the incoming-career result agree with hearing loss. They do not prove it.
- The turnover design assumes that, after controls, incoming and outgoing observers would have the same detection at equal tenure. Long-tenure observers came from earlier observer cohorts, and cohort skill can differ.
- Song frequencies come from xeno-canto recordings, not from BBS conditions. Some values are uncertain (Gray-cheeked Thrush, 14.6 kHz, is probably too high). Seventeen species had no frequency. The family-controlled STI-frequency slope is weaker (p = 0.09).
- The STI uses only temperature. GHCN_CAMS is interpolated at 0.5 degree. BBS counts are not detection-corrected in other ways (for example, time of day and weather).
- The count correction is linear in frequency, and the drift subtraction assumes a linear drift. The corrected ratios are therefore a range, not a single best value.
- The event-year and BCR x decade fixed-effect estimates were not the first pre-specified model. The plan named them as sensitivity variants. We report all variants.

## 7. Reproduce

1. `bash files/code/00_fetch.sh <scratch_root>` downloads the raw data into `<scratch_root>/datasets/` and prints hashes. In the campaign, the same files are in the shared store (see files/PROVENANCE.md).
2. `bash files/code/run_all.sh <root>`, where `<root>/datasets` holds the data. The scripts write intermediates to `<root>/work/scratch` and results to `<root>/work/result/files/results`. The run takes about 1.5 hours on one CPU core and needs about 4 GB RAM. We used Python 3.12.16, numpy 2.5.4, pandas 3.1.1, scipy 1.18.1, statsmodels 0.15.0, xarray 2026.9.0 and matplotlib 3.11.2.
3. The 2-draw first test of 05_final.py was replaced by the 150-draw run. The bootstrap seed is fixed (7). The route-half seed is 20261109.

## 8. Files

- files/ANALYSIS_PLAN.md: the plan written before the outcomes were calculated.
- files/results/main_results.json: P1-P4 (first pass; its P4 bootstrap uses the drift without fixed effects).
- files/results/robust_results.json: subsets and controls. Its "bcr_dec_fe" entries use dummy regression and have unusable SE. Use final_results.json for fixed-effect results.
- files/results/final_results.json and final_bootstrap_draws.csv: final estimates with absorbed fixed effects and 150 route-bootstrap draws.
- files/results/species_sti_frequency.csv, species_turnover_slopes.csv, species_slope_by_freq_bin.csv: species-level aggregates.
- files/results/turnover_by_tenure_bin.csv, tenure_by_year.csv: aggregate tables.
- files/figures/: Figures 1-4. files/code/: all code.
- files/PROVENANCE.md and files/NOTICE-external-data.md: sources, hashes, licences and attribution.

The event-level turnover table (route and observer numbers) and the run-level tables are not in the bundle. They are record-level derivatives of the BBS database. The scripts make them again.
