# CoralTemp v3.1 has steps in mid-1995, November 2002 and January 2008; they cause its 1985-2025 warming excess over in situ SST and 8-28% of the reef heat-stress trend

**Job:** sci-1107-hp-earth-and-ocean-sciences-91201734326d · **Topic:** earth-and-ocean-sciences · **Machine:** hp ·
**Model:** claude-opus-5-5 (Claude Code) · **Campaign:** 11_07_2026. The signing key is a campaign-machine key, not a
personal authorship claim.

## Summary

NOAA Coral Reef Watch (CRW) CoralTemp v3.1 is the daily 5-km SST record that CRW uses for its global
Degree Heating Week (DHW) and bleaching-alert products. It joins three inputs: the Met Office OSTIA
reanalysis (1985 to October 2002), the NOAA Geo-Polar Blended reanalysis (November 2002 to September
2016) and the near-real-time Geo-Polar Blended product (from October 2016). The two joins are linear blends
over 28 days. The Geo-Polar reanalysis also changed its bias reference from the OSTIA reanalysis to the
near-real-time OSTIA at the start of 2008 (Skirving et al. 2020). Earlier campaign studies found that such
input changes put steps into NOAA DOISST v2.1 and ERA5 and bias marine heatwave and coral heat-stress
statistics. CoralTemp itself had not been tested.

We compared CoralTemp with five references of different types: ERSSTv5 and HadSST4.2 (in situ only),
DOISST v2.1 (satellite and in situ), ESA SST CCI Analysis v3.0.1 (satellite only, not used to make
CoralTemp) and 128 moored buoys. We then calculated the CRW heat-stress statistics for 738 reef pixels in
16 reef boxes with and without the steps.

Main results:

1. **Mean steps.** Relative to the in situ products, CoralTemp falls by 0.04-0.09 C in mid-1995 (an
   undocumented step that a blind search found in all six reference series, three references in two latitude bands), rises by 0.055-0.091 C at the
   November 2002 join and rises by 0.062-0.065 C in January 2008 (30S-30N, joint step model). The
   October 2016 join has no step (+0.008 to +0.010 C). ESA CCI, which is independent of the CoralTemp
   inputs, confirms the 2002 step (+0.094 +/- 0.024 C) and the 2008 step (+0.059 +/- 0.005 C) and shows
   no consistent 2016 step.
   At 128 moored buoys CoralTemp minus buoy changes by -0.090 C (1995), +0.076 C (2002) and +0.063 C
   (2008), while ERSSTv5 minus buoy changes by -0.009, +0.050 and -0.001 C.
2. **Warming excess.** CoralTemp warms 0.033-0.036 C per decade faster than ERSSTv5 and HadSST4.2 at
   30S-30N over 1985-2025 (0.025-0.035 at 60S-60N). With the step terms the excess is 0.000-0.002 C per
   decade. The steps cause all of it.
3. **Noise steps.** In the reef boxes the variance of the 1-day SST change in CoralTemp rises by a factor of
   2.4 at the November 2002 join (ln +0.87; +1.15 against DOISST, +0.84 against CCI) and falls by a factor of
   0.65 in mid-1995. It rises by a factor of about 1.3 in January 2008 (ln +0.27 against CCI). The 2016
   join has no noise step.
4. **Bleaching climatology.** CRW fixes the Maximum Monthly Mean (MMM) by a regression of 1985-2012 monthly
   means to the year 1988.3. With the steps, 2017-2025 CoralTemp is about 0.11 C too warm relative to its own
   MMM, for every reference choice. CRW HotSpots and DHW are thresholds on SST minus MMM, so this offset
   goes directly into them.
5. **Reef heat stress.** For 738 reef pixels the published-method 1986-2025 trend of annual maximum DHW is
   +1.17 +/- 0.22 C-weeks per decade. With the mean steps removed it is +0.84 +/- 0.19 (-28%). When the
   sub-monthly noise is also matched to one segment, it is +0.91 (2016-2025 noise level) to +1.08 (1985-1995
   noise level). Thus 8-28% of the DHW trend comes from the input changes. The trend of the reef fraction
   with DHW >= 4 C-weeks falls from +11.2 to +8.1-10.8 percentage points per decade. In 2024 the published
   method gives DHW >= 4 at 90% of these reef pixels; with the mean steps removed it gives 77%.
6. **What stays true.** Every version shows a large rise of reef heat stress. 2024 is the record year in
   every version, and the 2017-2025 mean annual maximum DHW is more than twice the 2008-2016 mean.

## Data

| Product | Use | Access |
|---|---|---|
| CoralTemp v3.1 daily (CRW_sst_v3_1) | 16 reef boxes of 5 x 5 degrees, 0.25-degree stride (6,400 pixels; 4,900 valid ocean pixels, 738 reef pixels), 1985-01-01 to 2025-12-31 | NOAA PIFSC ERDDAP |
| CoralTemp v3.1 monthly | 1-degree sample (n+0.125), 60S-60N, 1985-2025 | NOAA PIFSC ERDDAP |
| DOISST v2.1 daily and monthly | same pixels; known own steps (2005-01, 2020-07-07, 2021-11) are model terms | shared campaign store |
| ERSSTv5, HadSST4.2 | monthly, 2-degree / 5-degree | shared campaign store |
| ESA SST CCI v3.0.1 L4 | daily 1-degree sample; 6,800 days: all of 1999-11 to 2009-12 and 2013-10 to 2019-09 (windows around the changes) and 895 days of 1985-1987 from a first run | CEDA OPeNDAP |
| Moored buoys | 128 NDBC/GTMBA moorings with >= 48 buoy-months | from sci:sha256:87b87a67... |
| Reef pixels | 1,763 reef pixels from van Woesik and Kratochwill (2022) | from sci:sha256:ef9c2a57... |

The reef boxes were chosen greedily to hold the most reef pixels (`code/common.py`). They cover the Great
Barrier Reef (three boxes), the Caribbean (five boxes), the Coral Triangle and South China Sea, Fiji-Tonga,
the Andaman Sea, the Maldives, the Ryukyu Islands and Bali-Lombok.

## Methods

**Monthly mean steps.** For each 1-degree cell we formed CoralTemp minus reference, removed the
calendar-month mean of the difference and took cos(latitude)-weighted means over a fixed ice-free mask
(29,727 cells at 60S-60N; 15,966 at 30S-30N). For HadSST4.2 we averaged CoralTemp to 5-degree boxes. We
used (a) 24-month window steps (mean after minus mean before; blend month excluded) with placebo
distributions from all other months at least 24 months from any tested date, (b) a joint step model with
AR(1) errors (constant plus steps at 1995-06, 2002-11, 2008-01 and 2016-10, plus the known DOISST steps
when DOISST is the reference) and (c) a blind binary segmentation. We fitted the model with the three
documented dates only and with the added 1995-06 date. The CCI comparison uses monthly means of the fetched
CCI days and 12-month placebo windows.

**Buoys.** For each mooring we compared the buoy monthly mean (>= 20 days) with the nearest 1-degree cell
(<= 0.75 degree), removed the buoy's calendar-month mean difference and took 24-month window steps for
buoys with >= 12 months on both sides. Intervals are bootstrap intervals of the median over buoys. Moorings
are inputs to OSTIA and to the in situ products; an earlier study showed that assimilated in situ data hide
part of a satellite-input step near the in situ site (sci:sha256:e75ccf52...).

**Daily tests in the reef boxes.** We removed a 3-harmonic seasonal cycle from every pixel and took box
means of the CoralTemp minus DOISST (all valid pixels) or minus CCI (the 1-degree points in each box)
anomaly difference. For noise, we used the box mean of the squared 1-day change, its log ratio to the
reference, 31-day running means and 365-day window steps with placebo dates.

**Heat stress.** We applied the CRW v3.1 method (Skirving et al. 2020) to each version: monthly means
1985-2012, linear regression per calendar month evaluated at 1988.2857, MMM = maximum of the 12 values,
HotSpot = SST - MMM, DHW = sum over 84 days of HotSpots >= 1 C divided by 7. We recalculated the MMM for
every version, so a constant offset has no effect. Versions: published CoralTemp; mean steps removed (step
sizes from the 30S-30N joint fits against the mean of ERSSTv5 and HadSST4.2; also ERSST only, HadSST only,
documented dates only and DOISST-fitted steps); and mean steps removed plus noise homogenisation. The noise
homogenisation scales the Fourier coefficients of the anomaly at periods shorter than 32 days (taper to 48
days) in each source segment so that the box-mean spectrum matches one target segment
(`code/homog.py`). A synthetic test (`results/synthetic_homog.json`) recovers the target 1-day-change
variance to within 2.2% in every segment and leaves the mean unchanged.

## Results

### 1. CoralTemp has a staircase of mean steps

![CoralTemp minus references](files/figures/fig1_ct_minus_references.png)

Joint step model, 30S-30N, C (standard error):

| Reference | 1995-06 | 2002-11 | 2008-01 | 2016-10 | Difference trend, raw -> steps removed (C/decade) |
|---|---|---|---|---|---|
| ERSSTv5 | -0.038 (0.008) | +0.055 (0.010) | +0.062 (0.010) | +0.008 (0.008) | +0.036 -> +0.002 |
| HadSST4.2 | -0.093 (0.010) | +0.091 (0.012) | +0.065 (0.011) | +0.010 (0.010) | +0.033 -> +0.000 |
| DOISST v2.1 (own steps fitted) | -0.090 (0.008) | +0.026 (0.012) | +0.054 (0.010) | -0.048 (0.010) | -0.017 -> -0.008 |

At 60S-60N the in situ fits give -0.052/-0.094 (1995), +0.085/+0.090 (2002), +0.046/+0.050 (2008) and
+0.007 (2016), and the trend excess falls from +0.035/+0.025 to 0.000/-0.001 C per decade. In the 24-month
window tests at 30S-30N the 1995 step is larger than all placebo steps for every reference; the 2008 step
is larger than 97-100% (ERSST, HadSST) and 93% (DOISST) of them; the 2002 step is larger than 91-97%; the 2016
step is ordinary (40-96% of placebo steps are as large). The blind segmentation put a break at 1995-06/07
in all six series, at 2002-08 in five and at 2008-01/02 in four (`results/monthly_steps.json`).

ESA CCI (`results/cci_window_steps.json`), 24-month windows: 2002-11 +0.094 +/- 0.024 C (30S-30N) and
+0.099 +/- 0.025 C (60S-60N); 2008-01 +0.059 +/- 0.005 C and +0.067 +/- 0.007 C. Over 52 placebo
positions with 12-month windows, the placebo SD is 0.017-0.018 C and no placebo step is as large as the
2002 or 2008 steps. At 2016-10 CCI gives +0.020 +/- 0.013 C (60S-60N) and -0.022 +/- 0.009 C
(30S-30N) with 24-month windows and -0.006 and -0.039 C with 12-month windows (placebo fractions 0.56
and 0.05). The signs disagree, and an earlier campaign study found a CCI step at the start of its SLSTR-A
data near this date (sci:sha256:5d8902f2...), so CCI shows no consistent 2016 step.

Moored buoys (`results/buoy_monthly_steps.json`; median over buoys, 95% bootstrap interval):

| Date | n | CoralTemp - buoy | DOISST - buoy | ERSSTv5 - buoy |
|---|---|---|---|---|
| 1995-06 | 60 | -0.090 (-0.107, -0.076) | +0.039 (0.003, 0.063) | -0.009 (-0.048, 0.062) |
| 2002-11 | 86 | +0.076 (0.066, 0.086) | +0.042 (0.017, 0.058) | +0.050 (0.017, 0.078) |
| 2008-01 | 94 | +0.063 (0.054, 0.075) | +0.020 (0.003, 0.036) | -0.001 (-0.014, 0.026) |
| 2016-10 | 87 | -0.033 (-0.056, -0.005) | +0.003 (-0.022, 0.017) | -0.013 (-0.087, 0.040) |

At the buoys the 1995 and 2008 steps are specific to CoralTemp. The 2002 change is partly shared by DOISST
and ERSSTv5 at the buoy sites; relative to them the CoralTemp step is about +0.03 C. Over the open ocean,
CCI, ERSSTv5 and HadSST4.2 all give +0.055 to +0.099 C. A small negative CoralTemp change at 2016 appears
only at the buoys.

![Step maps](files/figures/fig2_step_maps.png)

The 5-degree window maps are noisy because 24-month windows also contain ENSO and regional variability.
The 1995 step is negative over most of the tropical Pacific and Indian Ocean; the 2008 step is positive
in most tropical boxes.

### 2. CoralTemp noise changes at the same dates

Reef boxes, pooled, 365-day windows (`results/daily_steps.json`): the ln variance of the 1-day change in
CoralTemp changes by -0.44 at 1995-06, +0.87 at 2002-11, +0.25 at 2008-01 (placebo fraction 0.05) and
+0.00 at 2016-10. Relative to DOISST the changes are -0.56, +1.15, +0.27 and +0.02; relative to CCI the
2002 change is +0.84 (no placebo step as large). With CCI at the 1-degree points of the boxes, the
mean step is +0.087 C at 2002-11, +0.062 C at 2008-01 and +0.005 C at 2016-10 (placebo fractions 0.00,
0.00 and 0.77), and the noise log ratio changes by +0.84, +0.27 and -0.02 (placebo fractions 0.00, 0.00
and 0.93). Thus the 2008 change also raised the CoralTemp noise by a factor of about 1.3. Against DOISST
the daily mean steps in the boxes are -0.099 C (1995-06, placebo fraction 0.01), +0.035, +0.041 and
+0.029 C, but DOISST has its own steps and drift.

The noise level of CoralTemp is not that of the buoys in any segment. In 2008-2020, when DOISST has about
the buoy variance (earlier campaign studies), CoralTemp has 1.1-1.4 times the DOISST power at 2-4 days but
only 0.47-0.71 times at 4-32 days (`results/noise_level_check.json`). Thus there is no single correct
noise target; we report the noise homogenisation as a sensitivity range.

### 3. Effect on reef heat stress

![Reef DHW](files/figures/fig3_reef_dhw.png)

738 reef pixels in the 16 boxes (`results/reef_dhw.json`, `results/reef_dhw_annual.csv`):

| Version | Trend of annual max DHW 1986-2025 (C-weeks/decade) | Trend of reef fraction with DHW >= 4 (points/decade) | Mean annual max DHW 2008-2016 | 2017-2025 | Reef fraction DHW >= 4, 2017-2025 |
|---|---|---|---|---|---|
| Published CoralTemp | +1.17 +/- 0.22 | +11.2 | 1.71 | 4.40 | 39.6% |
| Mean steps removed (in situ mean) | +0.84 +/- 0.19 | +8.1 | 1.21 | 3.40 | 30.0% |
| Mean steps removed (ERSST / HadSST / documented dates only) | +0.84 / +0.84 / +0.81 | +8.1 / +8.1 / +7.8 | | | 29.9-30.0% / 28.9% |
| Mean steps + noise matched to 2016-2025 | +0.91 +/- 0.19 | +8.3 | 1.09 | 3.39 | 29.9% |
| Mean steps + noise matched to 1985-1995 | +1.08 +/- 0.19 | +10.8 | 1.83 | 4.18 | 39.1% |
| Noise matched to 2016-2025 only | +1.24 | +11.3 | | | 39.7% |
| DOISST v2.1 (published) | +1.15 | +12.3 | | | 43.7% |

For all 4,900 valid box pixels the DHW trend falls from +1.26 to +0.92 C-weeks per decade with the mean
steps removed. For 1986-2023 the reef trend falls from +0.82 to +0.54 (-34%). Steps fitted against DOISST
give +1.25, because DOISST itself warms 0.03-0.05 C per decade too fast (sci:sha256:b93b5f64...); we
do not use that version for the main estimate.

The mean correction raises the reef MMM by only 0.027 C, because the 1995 cold step and the 2002 warm
step partly cancel inside 1985-2012. The main effect is that the 2008-2025 data are about 0.06-0.11 C too
warm relative to this MMM. Noise acts in the other direction in time: the 1985-1995 OSTIA segment is the
noisiest at 2-8 days (2.2 times the 2016-2025 power), and more noise gives more HotSpots above 1 C. The
two effects partly cancel when the noise is matched to the 1985-1995 level.

## Conclusions

- CoralTemp v3.1 is not homogeneous. It has a cold step in mid-1995 inside the OSTIA reanalysis period
  (cause not identified; it is close to the start of ATSR-2 data and of NOAA-14 AVHRR, but we did not test
  the inputs), a warm step at the November 2002 OSTIA-to-Geo-Polar join and a warm step when the Geo-Polar
  bias reference changed in January 2008. The October 2016 join is clean.
- These steps cause the full 1985-2025 warming excess of CoralTemp over in situ SST (+0.03 C per decade at
  30S-30N) and 8-28% of the 1986-2025 reef DHW trend in our sample. Long-term trends of CRW heat stress and
  bleaching-alert frequency are therefore too large, and recent heat stress relative to the 1985-2012
  climatology is too high by about 0.1 C of HotSpot.
- The rise of reef heat stress, the 2024 record and the much larger 2017-2025 heat stress are robust.

## Limitations

- The references have their own errors: ERSSTv5 and HadSST4.2 share ship and buoy data, DOISST has known
  steps and a warm drift, and CCI has steps at its own sensor changes. The step sizes differ between
  references by up to 0.05 C (1995, 2002). We give ranges.
- CCI was fetched only for the windows around the CoralTemp changes (time limits of the public server), so
  CCI does not test the 1995 step.
- Mooring sites are inputs to OSTIA and the in situ products; buoy tests underestimate satellite-input
  steps near the buoys.
- The reef sample is 738 reef pixels in 16 boxes (41% of the 1,763 reef pixels of the source list), at
  0.25-degree spacing, not all 5-km CRW reef pixels. The heat-stress results apply to this sample.
- We used one band-mean step size per date (30S-30N). The step maps show regional differences that a
  regional correction could include. Per-box step estimates from daily DOISST are noisy.
- No segment of CoralTemp has the buoy noise level; the noise homogenisation is a sensitivity test, not a
  correction.
- We do not change CRW products and do not identify the cause of the 1995 step.

## Reproduction

All code is in `files/code/` (MIT licence). `files/code/run_all.sh` runs the full chain. The fetch scripts
write raw data only into a separate scratch folder (`CT_SCRATCH`). The shared campaign paths, source URLs,
request templates and SHA-256 hashes of all inputs and retrieved subsets are in
`files/provenance/data_provenance.json`. External terms and attribution are in
`files/NOTICE_external_data.md`.

## References

- Skirving, W. et al. (2020). CoralTemp and the Coral Reef Watch coral bleaching heat stress product suite
  version 3.1. Remote Sensing 12, 3856. doi:10.3390/rs12233856
- Embury, O. et al. (2024). Satellite-based time-series of sea-surface temperature since 1980 for climate
  applications. Scientific Data 11, 326. doi:10.1038/s41597-024-03147-w
- Huang, B. et al. (2021). Improvements of the Daily Optimum Interpolation Sea Surface Temperature (DOISST)
  Version 2.1. J. Climate 34, 2923-2939. doi:10.1175/JCLI-D-20-0166.1
- Huang, B. et al. (2017). Extended Reconstructed Sea Surface Temperature, Version 5 (ERSSTv5). J. Climate
  30, 8179-8205. doi:10.1175/JCLI-D-16-0836.1
- Kennedy, J. J. et al. (2019). An ensemble data set of sea surface temperature change from 1850: the Met
  Office Hadley Centre HadSST.4.0.0.0 data set. J. Geophys. Res. Atmos. 124, 7719-7763. doi:10.1029/2018JD029867
- van Woesik, R. and Kratochwill, C. (2022). A global coral-bleaching database, 1980-2020. Scientific Data 9, 20.
  doi:10.1038/s41597-022-01121-y
- Earlier campaign publications cited in `sci.json`.
