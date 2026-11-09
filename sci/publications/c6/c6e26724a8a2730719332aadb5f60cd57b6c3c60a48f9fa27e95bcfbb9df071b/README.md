# Tide gauges recorded clear earthquake offsets at few sites, and only Tohoku 2011 changed decadal sea-level rates, in a global PSMSL screen for 1900-2025

**Job:** sci-1107-dell-earth-and-ocean-sciences-990600092855 · **campaign:** 11_07_2026 · **topic:** earth-and-ocean-sciences · **machine:** dell · **model:** Claude Opus 5.5 (claude-opus-5-5) through Claude Code · **date:** 2026-11-08.
The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question

Earthquakes move the land under tide gauges. Then the relative sea level (RSL) at the gauge changes in one step, and it can continue to change for years (postseismic motion). Sea-level studies use tide-gauge trends, so it is important to know how frequently and how strongly earthquakes change these records. Regional studies exist (for example 38 western North Pacific gauges, Klos et al. 2019, GPS Solutions, doi:10.1007/s10291-019-0896-1). We did not find a global screen with a stated noise model.

We asked three questions:

1. After shallow earthquakes of magnitude (M) 6.5 or more, how many tide gauges show an initial RSL offset above the gauge noise?
2. After shallow M 7.5 or more earthquakes, how many gauge sites show a change in the 10-year RSL rate?
3. When an offset is clear, how much of it reverses in the next 10 years?

## Data

* PSMSL Revised Local Reference (RLR) monthly mean sea level, 1,633 stations, file version of 2026-10-19 (shared dataset `psmsl-rlr-monthly-20261108`, sha256 `b22f65f5…`). We removed months that PSMSL marks with the "flag for attention".
* USGS ComCat, all events M ≥ 6.5 from 1900 to 2026-11-01 (one fdsnws query; exact bytes in `files/data/raw/`). We used earthquakes with depth ≤ 70 km before 2026-01-01.
* Smithsonian GVP Holocene volcano list (shared dataset `gvp-votw-holocene-volcanoes-20261108`) for a volcano filter.

`files/data/provenance.json` gives URLs, dates and hashes.

## Method

**Rupture scale.** For each earthquake, L = 10^(−2.44 + 0.59 M) km (Wells & Coppersmith 1994 surface rupture length). "Near" gauges are ≤ 1.5 L from the ComCat epicentre (minimum 30 km). "Control" gauges are 3 L to 6 L from the epicentre. The control pairs use the same events, epochs and gauge network, but they are too far for a large tectonic signal.

**Ocean reference.** Ocean variability is common to gauges in a region. When possible, we subtracted the median monthly anomaly of gauges ≤ 1000 km from the target and ≥ 3 L from the epicentre. For great earthquakes (for example Tohoku, L = 849 km) no such gauge exists, so we used the raw series. Figure 1 shows raw series.

**Initial offset (question 1, M ≥ 6.5, `02_pairs.py`).** We fitted a line plus annual and semiannual terms to the 10 years before the event month (≥ 60 months, ≥ 5-year span). The initial offset O is the mean residual in months 1–6 after the event, so it includes early postseismic motion. We repeated the same calculation at placebo dates of the same gauge (every 3rd month within ±50 years, not within ±3 years of a near M ≥ 6.5 event). The robust SD of the placebo offsets (1.4826 × MAD) gives z = O/SD. We excluded a pair when a larger near event occurred in the same month or in the 24 months before. A later comparable event (M ≥ M_event − 0.5) cuts the post-event windows.

**Rate change (question 2, M ≥ 7.5, `04_rates.py`).** We merged PSMSL series within 10 km into one site, and we gave each series its own intercept. Thus a datum break at the event (for example a new "II" series) does not bias the slope. dRate = slope in years +1 to +11 minus slope in years −15 to 0 (≥ 96 months over ≥ 8 years before; ≥ 60 months over ≥ 6 years after).

**Test.** For each statistic we fitted a Student-t distribution (location 0) to the control-ring values. This gave two-sided p-values for the near pairs. Then we applied Benjamini–Hochberg (BH) at a false-discovery rate of 10%. We also compared the near and control distributions with a one-sided Mann–Whitney test.

**Filters (decided after inspection).** The first control distributions had heavy tails. The causes were volcanic islands (Miyake-jima, Kozu-shima: dike intrusion in 2000) and control pairs that were near a different earthquake. Thus the main analysis removes sites within 25 km of a volcano with an eruption since 1500 CE (in both classes). It also removes control pairs with another shallow event (M ≥ 6.5 for offsets, M ≥ 7.0 for rates) near the site in the analysis windows. We made this filter after we saw the data. Thus we also give the unfiltered results.

**Reversal (question 3).** For pairs with a clear offset, the reversed fraction is −(W_k − O)/O. W_k is the mean residual (relative to the extrapolated pre-event trend) in years 0.5–2, 2–5 and 5–10.

## Results

### 1. Initial offsets are rarely above noise (Figure 2, left)

| | near (≤ 1.5 L) | control (3–6 L) |
|---|---|---|
| event–gauge pairs with usable data | 277 (114 events) | 182 |
| \|z\| ≥ 3 | 7 (2.5%) | 1 (0.5%) |
| BH discoveries at FDR 10% | **6** | – |
| Mann–Whitney, \|z\| near > control | p = 0.089 | |

Out of 1,829 geometric near pairs, only 277 had enough data before and after the event. The 6 discoveries come from 5 earthquakes:

| event | gauge | O (mm) | z |
|---|---|---|---|
| Tohoku M9.1, 2011 | Ofunato II | +757 (RSL rise = land subsidence) | 37.0 |
| Tohoku M9.1, 2011 | Onahama | +497 | 22.8 |
| Niigata M7.6, 1964 | Nezugaseki | +193 | 5.4 |
| central Chile M7.8, 1971 | Valparaíso | −198 (land uplift) | −4.9 |
| Guantánamo M6.6, 1947 | Guantánamo Bay | −112 | −3.9 |
| Rat Islands M8.7, 1965 | Massacre Bay (Attu) | +123 | 3.8 |

The offsets come mostly from the gauges nearest to the epicentre: 4 of the 6 discoveries are in the 37 pairs at < 0.5 L (Ofunato 0.11 L, Onahama 0.24 L, Nezugaseki 0.31 L, Valparaíso 0.43 L). Only 2 are in the 240 pairs at 0.5–1.5 L (Massacre Bay 0.84 L, Guantánamo Bay 1.38 L). Without the filters, BH gives 3 discoveries (the two Tohoku gauges and Nezugaseki).
The Guantánamo 1947 offset comes from one gauge with a short reference. It can be a datum problem. We did not confirm it with another source.

### 2. Only Tohoku 2011 changed decadal RSL rates beyond control noise (Figures 2 right and 3)

| | near | control |
|---|---|---|
| site–event pairs | 166 (38 events) | 275 |
| robust SD of dRate | – | 5.1 mm/yr (t fit: df 4.2, scale 5.2 mm/yr) |
| \|dRate\| ≥ 15 mm/yr | 8.4% | 4.0% |
| BH discoveries at FDR 10% | **4, all Tohoku 2011** | – |
| Mann–Whitney, \|dRate\| near > control | p = 0.038 (p = 0.011 without Tohoku) | |

The four discoveries are Ayukawa (−63 mm/yr: +9.0 before, −53.9 after), Ofunato (−46), Kamaishi (−36) and Soma (−34 mm/yr). Miyako (−25) and Onahama (−22 mm/yr) do not pass BH. All these sites are within 0.25 L of the Tohoku epicentre. A negative dRate means that the land started to rise after the event. Thus the coast that subsided in 2011 rose quickly in 2012–2021. This agrees with GNSS reports of postseismic uplift on the Tohoku coast. At 0.25–1.5 L the median |dRate| (3.5–5.3 mm/yr) is close to the control value (3.5 mm/yr). The weak Mann–Whitney excess without Tohoku shows that small rate changes can occur at more sites. But no single site other than the Tohoku sites passes BH. Other large values (Adak 1957, −19 mm/yr; Lyttelton after Kaikoura 2016, −17 mm/yr; Ko Taphao Noi after Sumatra 2004, +16 mm/yr) are inside the control tail. Without the filters, BH gives no rate discoveries, because the volcanic control sites have rate changes of up to 243 mm/yr.

### 3. Tohoku offsets reversed by about 45% after 5–10 years

| gauge | O (mm) | reversed, yr 0.5–2 | yr 2–5 | yr 5–10 |
|---|---|---|---|---|
| Ofunato II (Tohoku) | +757 | 0.06 | 0.20 | 0.47 |
| Onahama (Tohoku) | +497 | 0.15 | 0.24 | 0.45 |
| Adak (Andreanof M8.6, 1957; z 3.1, not BH) | +158 | 0.33 | 0.70 | 1.00 |
| Guantánamo Bay (1947) | −112 | 0.34 | 0.26 | 0.35 |
| Nezugaseki (Niigata 1964) | +193 | −0.05 | 0.04 | −0.14 |

The reversal is relative to the extrapolated pre-event trend. Selection on O can cause a regression-to-the-mean bias. We estimated it from the placebo covariance of later change and O. It is ≤ 0.014 for the two Tohoku gauges and ≤ 0.1 for the other pairs. The Tohoku reversal was still continuing at the end of the record (Figure 1). Niigata 1964 had no reversal in 10 years. There are too few clear cases to give a general reversal rate.

### 4. PSMSL series do not end more frequently near large earthquakes

Of 372 gauges active 0.5 year before a near M ≥ 7.5 event, 7 (1.9%) ended within [−0.5, +1] year. Of 1,987 control gauges, 1.9% ended (Fisher p = 1.0). The value at placebo dates for the same near gauges was 1.2%. Thus PSMSL does not systematically end RLR series at earthquakes. But data gaps after destructive tsunamis (for example Ayukawa has no months 1–6 after 2011) remove many offsets from test 1.

## Interpretation

In the PSMSL record, earthquake signals above the tide-gauge noise are rare. They occur only at the few gauges within about 0.5 rupture lengths of large shallow earthquakes. Most of the evidence comes from one event, Tohoku 2011. For most gauges and most earthquakes, the monthly noise (SD of the 6-month offset 20–50 mm, SD of the decadal rate change about 5 mm/yr) is larger than the expected tectonic signal. Thus a sea-level study that removes or models only the gauges within about 0.5 L of large events will not miss many detectable earthquake effects. But the Tohoku coast shows that a near-field gauge can change its rate by 30–60 mm/yr for a decade. Then a linear trend that crosses such an event is not a valid estimate of vertical land motion.

## Limitations

* Data coverage is the main limit. Many famous events (Alaska 1964, Chile 1960 and 2010, Sumatra 2004, Peru 2001) have no near gauge with 5–10 years of data before and data in the first months after. Thus the screen cannot say whether these events changed the gauge records.
* Distance is measured from the ComCat epicentre, not from the rupture surface. For long ruptures, the near class contains many gauges far from the slip. We did not use slip models or Okada predictions.
* Monthly RSL includes ocean variability. The regional reference is not available for great earthquakes. Thus the Tohoku and Sumatra values use raw series.
* The volcano and other-event filters were chosen after we saw the control tail. We report the unfiltered counts above. The t-fit null is a model of the control tail; with 182 and 275 control pairs, the far tail of this model is uncertain.
* The offset includes months 1–6, so it mixes coseismic and early postseismic motion. Datum changes at gauge repair can look like offsets; we did not check gauge metadata event by event.
* The rate test ends 11 years after the event, so events after 2014 have shorter post windows or none.

## Files

* `files/code/` – `01_load.py` (read PSMSL and ComCat), `02_pairs.py` (offsets and placebo SD), `03_summary.py` (one row per pair), `04_rates.py` (site rate changes), `05_splits.py` (series ends), `07_stats.py` (filters, t-fit null, BH, `summary.json`), `06_figures.py`, `run_all.sh`.
* `files/data/raw/comcat_m6.5_1900_2026.csv.gz` – exact ComCat bytes used.
* `files/data/derived/` – all event–gauge pair tables (`pairs_m6.5`, `pairs_best`, `pairs_best_filtered`), site rate tables (`rates_m7.5`, `rates_filtered`), `sites`, `gauges`, `quakes`, `series_ends`.
* `files/results/summary.json` – all numbers in this README; `offset_near_pairs_ranked.csv` and `rate_near_pairs_ranked.csv` – near pairs ranked by p.
* `files/figures/` – Figures 1–3.

## Reproduce

Run `files/code/run_all.sh` from a directory with `datasets/` (PSMSL zip and GVP CSV, see hashes) and `work/code/` (copy of `files/code`). The script uses the archived ComCat bytes or a new fdsnws query (new queries can differ slightly because ComCat changes). Python 3.12 with numpy 2.5, pandas 3.1, scipy 1.18, matplotlib 3.11, pyarrow 26. The two pair scripts take 10–25 minutes each on a loaded 24-core host (single thread).
