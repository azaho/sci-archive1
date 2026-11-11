# NHC rapid-intensification probabilities (2020-2025): the SHIPS-RII consensus was calibrated over water, but its members had opposite errors and all SHIPS-RII models ignored land

Job: sci-1107-hp-earth-and-ocean-sciences-cf978b3c7eb4 · topic: earth-and-ocean-sciences · machine: hp · account: claude-olen · model: Claude Opus 5.5 (claude-opus-5-5) · date: 2026-11-11.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## 1. Question

This work continues the campaign series that verifies public hazard products (PAGER, ShakeMap, ShakeAlert, USGS aftershock forecasts, NHC track circles, wind speed probabilities and formation probabilities, SWPC and Coral Reef Watch probabilities). The series had not tested the rapid-intensification (RI) guidance of the US National Hurricane Center (NHC). NHC forecasters use this guidance for intensity forecasts. RI is an increase of the maximum wind of at least 30 kt in 24 h (and seven other thresholds).

We asked two questions:

1. Are the operational RI probabilities calibrated against the final best track?
2. If they are not calibrated, which physical or algorithmic property of each model causes the error?

## 2. Data

* **Forecasts.** The `RI` records in the public NHC ATCF e-decks, `https://ftp.nhc.noaa.gov/atcf/archive/YYYY/e{al,ep,cp}NNYYYY.dat.gz`. The archive has RI records only for 2020-2025 (the 2005-2019 e-decks have none). We used 237 e-deck files. Their SHA-256 values are in `files/provenance/edeck_2020_2025_sha256.txt`. Techniques:
  * `RIOD`: SHIPS-RII, linear discriminant (Kaplan et al. 2010).
  * `RIOL`: logistic regression model.
  * `RIOB`: Bayesian model.
  * `RIOC`: arithmetic mean of the three (Kaplan et al. 2015).
  * `EIOD`/`EIOL`/`EIOB`/`EIOC`: the same models with ECMWF fields.
  * `DTOP`: DTOPS (deterministic-to-probabilistic model).
  * `DTPE`: a DTOPS variant (2020-2023 only).
  * `SDCN`/`SDCE`: new consensus models (2024-2025 only).
  
  Each record gives the probability, the intensity change dV, the window and the final intensity. Thus each record also gives the operational initial intensity, V_op0 = V - dV.
* **Truth.** Final HURDAT2 (NHC public domain):
  * Atlantic 1851-2025, file `hurdat2-1851-2025-092326.txt`, sha256 `75202780…6b4`.
  * NE/C Pacific 1949-2025, file `hurdat2-nepac-1949-2025-092926.txt`, sha256 `caece626…507`.
  
  We used the shared campaign copies (`datasets/nhc-hurdat2-*`).
* **Land.** Natural Earth 10 m land v5 (public domain), shared `datasets/naturalearth-10m-land-v5/ne_10m_land.zip`, sha256 `e547d749…dc`.
* **Issue-time track.** The TVCN consensus track positions at 12, 24, 36, 48 and 72 h. These positions are `TR` records in the same e-decks.
* **Model code.** We examined the NCEP/NCO operational source `nhcg.v5.2.0` (`sorc/iships.fd/iships.f`, `rapidga.f`, `rapidbaya_2018.f`, `rapidloga_2018.f`, `dtops.fd/dtops_realtime.f`; SHA-256 values are in `files/provenance/nco_source_sha256.txt`). We did not bundle this code.

**Event definition (pre-registered).** RI occurred when the best-track endpoint change V(t0+tau) - V(t0) was at least dV. We used synoptic times only. At t0, the best-track status had to be TD, TS, HU, SD or SS. A best-track point had to exist at t0+tau. We excluded invests.

**Sample.** For the main 30 kt / 24 h RIOC test there were:
* Atlantic: 2,126 forecasts from 119 storms, with 123 RI events.
* Eastern + central Pacific (EP): 1,835 forecasts from 112 storms, with 154 RI events.

**Uncertainty.** All intervals are 95% storm-block bootstrap intervals (1,000 draws).

## 3. Pre-registration

We wrote `files/provenance/PREREG.md` and recorded its hash before we computed any statistic. At that time we had inspected only the record format and one 2023 file. The plan fixed these items:
* the primary metric, observed/expected event count (O/E);
* the reliability bins and the Brier skill score;
* source tests S1-S5;
* a secondary prospective recalibration test (train 2020-2022, test 2023-2025).

Deviations:

1. The plan gives HURDAT2 revision dates as "2026-03-23/29". The correct dates are 2026-09-23/29 (file-name suffix MMDDYY). The files are unchanged.
2. We added these items after we saw the first results. They are exploratory:
   * a land test with a land mask (along the best track and along the issue-time TVCN track);
   * the issue-time land rule in the prospective test;
   * a check of the operational source code;
   * strength bins over water;
   * SDCN/SDCE, which first appeared in the data.

## 4. Results

### 4.1 Overall calibration, 30 kt / 24 h (pre-registered)

| Technique | Atlantic O/E (95% CI) | EP O/E (95% CI) | BSS AL / EP |
|---|---|---|---|
| RIOD (SHIPS-RII discriminant) | 0.55 (0.40-0.72) | 0.64 (0.49-0.80) | 0.10 / 0.17 |
| RIOL (logistic) | 0.72 (0.52-0.91) | 1.15 (0.90-1.42) | 0.06 / 0.19 |
| RIOB (Bayesian) | 1.68 (1.30-2.17) | 2.36 (1.74-3.42) | 0.13 / 0.13 |
| RIOC (consensus) | 0.79 (0.58-1.00) | 1.05 (0.82-1.28) | 0.15 / 0.23 |
| EIOC (ECMWF consensus) | 0.81 (0.59-1.05) | 0.95 (0.75-1.16) | 0.14 / 0.24 |
| DTOP (DTOPS) | 0.97 (0.75-1.21) | 1.15 (0.92-1.41) | 0.22 / 0.28 |
| SDCN (2024-2025) | 1.16 (0.69-1.59) | 1.14 (0.68-1.52) | 0.29 / 0.26 |

O/E < 1 means that the probabilities were too high. BSS is the Brier skill score against a leave-one-year-out basin climatology. The full tables for all 8 thresholds are in `files/results/oe_all_thresholds.csv`, and the reliability bins are in `reliability_30kt24h.csv` (Figure 1).

* The consensus RIOC was near calibrated. Its three members were not. RIOD gave 1.5-2 times too many expected events (O/E 0.50-0.67 at every threshold in both basins, except 0.81 for 20 kt/12 h in the Atlantic). RIOB gave 1.4-5.6 times too few, and this error increased with threshold (EP 40 kt/24 h: O/E 5.1).
* The consensus is therefore right because opposite member errors cancel. The campaign found the same pattern for ShakeAlert contours.
* DTOPS was calibrated in both basins and had the highest skill.

### 4.2 Source 1: the Bayesian member is over-confident

We fitted calibration slopes, logit(obs) = a + b·logit(p) (`calibration_slopes_30kt24h.csv`). Results:
* RIOB: b = 0.73 (0.57-0.86) for the Atlantic and 0.65 (0.54-0.79) for the EP. A slope below 1 means that the probabilities are too extreme.
* RIOB gave ≤1% in 74-83% of forecasts. Yet 82 of the 277 RI events (30%) came after a RIOB value of ≤1%.
* In 184 forecasts, RIOB gave ≤1% while RIOD gave ≥20%. RI followed in 18% of these forecasts.

This behaviour agrees with a Bayesian classifier that multiplies predictor likelihoods as if the predictors were independent. Such a classifier pushes probabilities to 0 and 1.

The discriminant RIOD had a slope near or above 1 (AL 1.43, EP 1.10). Its probabilities were too high at all levels, most clearly between 5% and 20%: the observed rates in that range were 1.5-5%.

### 4.3 Source 2: SHIPS-RII ignores land (pre-registered S2 and exploratory land tests)

We first used the pre-registered HURDAT2 landfall flags. In windows with a landfall, RIOC had O/E 0.38 (0.15-0.61) in the Atlantic and 0.39 (0.12-1.01) in the EP. In the other windows the values were 0.91 and 1.10. The stated direction (over-forecast near land) was confirmed.

We then used an issue-time land flag: did the TVCN track, from the t0 position to the 24-h position, cross Natural Earth land? This flag needs only data that exist when the forecast is issued. 12% of the windows crossed land. The flag agreed with the best-track land flag in 97% of windows (Figure 2, `S2b_land_oe.csv`).

* **Atlantic, land-crossing windows.** The mean RIOC probability was 8.9%, but the observed RI rate was 1.4%: O/E 0.16 (0.03-0.30), with 6 events against 37.7 expected. The SHIPS-RII probabilities over land were *higher* than over water (8.9% against 7.0%).
* **EP, land-crossing windows.** There were 0 events against 5.3 expected.
* **Over-water windows.** RIOC had O/E 0.99 (0.72-1.26) in the Atlantic and 1.09 (0.84-1.35) in the EP. Thus the whole Atlantic over-forecast of the consensus came from land-crossing windows. These windows were 20% of the cases but contributed 24% of the expected events.
* **DTOPS.** DTOPS lowered its probabilities over land (mean 3.1% in the Atlantic). It had O/E 0.50 (0.12-1.01) there.
* **All thresholds.** The same pattern occurred at all 8 thresholds from 20 kt/12 h to 65 kt/72 h (Figure 3, `oe_land_all_thresholds.csv`). Over land, RIOC had Atlantic O/E 0.10-0.36, with mean probabilities 2.8-10 times the observed rate. In the EP it had O/E 0-0.22. Over water, RIOC had O/E 0.98-1.38.

**Why.** The NHC JHT reports of Kaplan et al. state that the RI models were developed and verified on over-water cases only ("for all systems that remained over-water during the specified forecast lead-time"). The operational code (`iships.f`, nhcg.v5.2.0) calls the RI routines and writes `RIOD`/`RIOL`/`RIOB`/`RIOC` to the e-deck. We found no land check on this path, and the RI routines take no land or track input. Thus a probability that is conditional on an over-water track is issued for every forecast.

DTOPS is different. It uses the 24-h intensity changes of DSHP, LGEM, HAFS, GFS and ECMWF. These forecasts already include land decay or land surfaces, so DTOPS inherits a land response. This is a specific algorithmic source of error. A simple land rule can remove it (Section 4.6).

### 4.4 Source 3: initial-intensity mismatch is not a main source (pre-registered S1)

The operational initial intensity was below the final best-track value in 18% of forecasts and above it in 10% (mean −0.4 kt). We repeated the test with the truth defined as V_bt(t0+24) - V_op0 ≥ dV. RIOC then changed from 0.79 to 0.85 (AL) and from 1.05 to 1.17 (EP). The |log O/E| did not fall by half. By the pre-registered rule, this mismatch is therefore not a main source (`S1_oe_opinit.csv`).

### 4.5 Other pre-registered and exploratory results

* **Storm strength over water (S3, exploratory refinement).** In the Atlantic, RIOC over-forecast RI for depressions below 35 kt: O/E 0.36 (0.07-0.75). It under-forecast RI for 64-95 kt hurricanes: O/E 1.80 (1.31-2.39). DTOPS had no such error (1.04, 0.73-1.33) (`S3b_v0bins_overwater.csv`).
* **Year-to-year variation (S4).** Yearly O/E followed the yearly RI frequency (RIOC, r = 0.80 AL and 0.96 EP), and the mean forecast followed it less closely (r = 0.51 / 0.68). For example, the EP in 2023 had RI in 14% of forecasts and O/E 1.61 (1.09-2.20). The guidance does not capture season-to-season changes in RI frequency.
* **GFS against ECMWF fields (S5, homogeneous sample).** The EIO* versions behaved like the RIO* versions: the same member pattern and similar BSS.

### 4.6 Prospective test, 2023-2025 (secondary)

We trained on 2020-2022 and tested on 2023-2025 (`prospective_2023_2025.csv`).

* **Two-parameter logistic recalibration (pre-registered).** This recalibration did *not* help. Over 96 technique × basin × threshold combinations, the Brier score became worse in 70 (significantly worse in 13, significantly better in 10). The cause is that 2023-2025 had more RI than 2020-2022 (raw RIOC EP test O/E 1.27).
* **Issue-time land rule (exploratory).** This rule replaced each forecast in a land-crossing TVCN window with the training-period land event rate. It improved the Brier score of RIOC in all 16 threshold × basin cases (95% CI below zero in 10 cases, never above). It did the same for RIOD (16/16, 10 significant), RIOL (16/16, 8 significant) and EIOC (16/16, 9 significant). For 30 kt / 24 h RIOC in the Atlantic, the Brier score decreased by 0.0013 (0.0005-0.0023), which is 2.6%. For DTOPS the rule gave no gain (7 of 16 negative).
* **Interpretation.** The land error is stable and can be removed. The members' level errors, in contrast, change with the season's RI frequency.

## 5. Limitations

* Only six seasons (2020-2025) have archived RI records. In each basin there are about 120 RI events per technique. Thresholds above 35 kt have 50-110 events, and 2024-2025-only models (SDCN/SDCE) have fewer than 50.
* The truth is the final best track at 6-h endpoints. Peak-within-window RI and non-synoptic records are not used. Best-track intensity has its own error (about 5-10 kt for storms without aircraft data).
* The issue-time land flag uses the TVCN consensus track and the best-track t0 position (which is close to the operational position), with straight lines between fixes. Small islands and coastline crossings shorter than 1 h can be missed. NHC's own land check, if one is applied at a later stage, may differ.
* For the EP, the training period had no RI events in land-crossing windows, so the land rule set those probabilities to 0. In a longer record this value would be small but not zero.
* We do not know how NHC forecasters weight the individual members. A miscalibrated member matters only to the degree that forecasters read it as a probability.
* The 2026 operational code (nhcg.v5.2.0) calls new "structure" versions of the discriminant model (`rapidga_structure`). Our sample covers 2020-2025, and the code check describes the current path. We did not have the 2020-2025 versions of the code.
* The Bayesian-overconfidence explanation is based on the calibration slope and the ≤1% floor. We did not inspect the internals of the Bayesian likelihood tables.

## 6. Reproduction

`files/code/run_all.sh SCRATCH_DIR DATASETS_DIR` downloads the 2020-2025 e-decks and b-decks from the NHC ATCF archive into SCRATCH_DIR (about 10 minutes over IPv4). It then runs scripts 01-06 (about 3 minutes with 1 CPU) and writes `out/*.csv` and `fig/*.png`.

* We tested a re-run from the bundled code against the bundled tables. It reproduced them exactly (seeded bootstraps).
* NHC can re-issue archive files. Compare the new hashes with `files/provenance/edeck_2020_2025_sha256.txt`.

Scripts:
* `01_build_cases.py` parses the RI records and matches them to HURDAT2.
* `02_verify.py` computes the pre-registered O/E, reliability, BSS and S1-S5.
* `03_sources.py` computes the land flags, calibration slopes and the Bayesian-floor summary.
* `04_prospective_and_thresholds.py` computes the issue-time land for all windows and the 2023-2025 test.
* `05_figures.py` makes the figures.
* `06_extra.py` computes the strength bins over water and the yearly correlations.

`files/results/cases_30kt24h.csv.gz` is the case-level table for 30 kt / 24 h (38,602 rows, all techniques). It is derived only from public-domain NOAA data (see `files/NOTICE_external_data.md`).

## 7. References

* Kaplan, J., M. DeMaria, J. A. Knaff, 2010: A revised tropical cyclone rapid intensification index for the Atlantic and eastern North Pacific basins. Wea. Forecasting 25, 220-241. doi:10.1175/2009WAF2222280.1
* Kaplan, J., et al., 2015: Evaluating environmental impacts on tropical cyclone rapid intensification predictability utilizing statistical models. Wea. Forecasting 30, 1374-1396. doi:10.1175/WAF-D-15-0032.1
* Kaplan et al., NHC Joint Hurricane Testbed final report (2013), https://www.nhc.noaa.gov/jht/11-13reports/Final_Kaplan_JHT13.pdf
* NCEP/NCO NHC guidance source nhcg.v5.2.0, https://www.nco.ncep.noaa.gov/pmb/codes/nwprod/nhcg.v5.2.0/
* ATCF e-deck format, https://science.nrlmry.navy.mil/atcf/docs/database/new/edeck.txt
* Campaign publications that we cite in `sci.json` (PAGER, ShakeAlert, aftershock, NHC circle, wind speed probability and formation probability verifications).
