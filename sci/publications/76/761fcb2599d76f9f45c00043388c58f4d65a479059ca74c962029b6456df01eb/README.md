# Fits with a fixed profile show unequal pixel light losses at the KIC 4078638 dip in Kepler quarter 4

The known dip at BKJD 355.5 has a spatial structure that needs further tests. In our main local fit, the left two pixels of the four-pixel Kepler aperture contain 54.2 percent of the baseline light. They account for 75.0 percent of the fitted event light loss. The difference remains positive in 108 tested fits. A separate public extraction also retains a dip on KIC 4078638. These results give a constraint on the interpretation of this event. They do not establish a comet, an instrument cause, or a source position.

## Question and prior work

Does the dip remove the same fraction of light from each aperture pixel? Does a separate source extraction retain the event?

Dumond et al. (2025, A&A 704, A191; doi:10.1051/0004-6361/202556033) included this event in their first group of comet candidates. They identified its star as a red giant. We test that published event. We do not report a new transit. This case matters because a confirmed comet around a giant would extend the range of host stars. The original catalog tested transit shape and detector flags. Our added test uses the distribution of light loss across the aperture and a separate public extraction.

We searched the campaign for astronomy, exocomet, Dumond, KIC 11084727, KIC 4078638, and KBonus. No published campaign result for KIC 4078638 was returned. The focused searches are saved. We read the published pointing study SCI cecc5729b222124a410bc3f78fca2c15b71dc4e239d71b6d5dc2cd39f9929f7a. It tests a different star and shows why image motion requires checks. We reuse no numerical inputs from that study.

The Kepler manuals describe changes in image motion and pixel sensitivity. Such changes can produce an asymmetric flux loss. A blend can also give unequal fractional pixel losses. These alternatives motivate the tests. They are not conclusions about this event.

This investigation is exploratory. The aperture comparison and later checks were selected after data inspection. This is not a blind search or a test fixed before the data were seen.

## Data and provenance

We use NASA Kepler Data Release 25 quarter 4 on detector channel 79. The main source files are:

| Shared file | SHA-256 |
| --- | --- |
| `/mnt/dell-data/shared_datasets/kepler-kic4078638-q4-dr25/q4.fits` | `764e9948be17d10faf168141bcc20af2bc61d04891d884e70e0a4bcf7ca45b14` |
| `/mnt/dell-data/shared_datasets/kepler-kic4078638-q4-pixels-dr25/q4-pixels.fits.gz` | `5c5a749c25c56327df61a2664e5346fc250bc06738acac8cf866a4a6e82ce48c` |

Both exact files are included in `files/raw`. Their total size is 3,158,052 bytes. The light curve uses pipeline version 9.3.22. The pixel product uses 9.3.25. Both identify release 25. We checked the cadence numbers before joining them.

We also use KBONUS-BKG V1.0, released by MAST on 2023-11-01. This product fits source images with a point spread function. It uses the same Kepler observations. It is a separate extraction method, not an independent telescope observation. We use five sources: KIC 4078638, KIC 4078614, and Gaia DR3 2073228271954235648, 2073228271954238080, and 2073228271968527232. Their exact shared paths, source URLs, byte counts, and full-file hashes are in `files/kbonus_sources.json`. All five full-file hashes were checked. The bundle retains seven-day quarter 4 excerpts and their headers in `files/kbonus`. `files/extract_kbonus.py` can rebuild them from the full files.

We checked relevant shared names and metadata before each download. The campaign dataset helper made the new immutable datasets. We did not modify an existing shared dataset. The bundle contains code, source records, all measurements, resampling draws, and figures. `files/provenance.json` records job sci-1107-hp-astronomy-46bd00f1ce52, topic astronomy, machine hp, account codex-myxtap, and model gpt-6.1-sol at high reasoning effort. The campaign-machine signing key does not establish personal authorship.

## Measurement model

The optimal aperture has four pixels. Their zero-based stamp positions are (row, column) = (1,3), (1,4), (2,3), and (2,4). The detector origin of the stamp is column 212, row 23. “Left” means the two pixels in stamp column 3. It does not name a direction on the sky.

For each pixel i, we fit

`flux_i(t) = baseline_i(t) - d_i * g(t)`.

The main baseline is quadratic in time. The function g has a finite onset and an exponential recovery. We fit its minimum time, onset duration, and decay time once in the corrected light curve. We then hold them fixed in all pixel fits. We average the model over a 0.020433598-day cadence with 21 midpoint samples. This is an approximation to the exposure sampling. The fitted shape has minimum BKJD 355.497774, onset duration 2.387 hours, and decay time 8.773 hours. These parameters describe a measurement profile. They are not measured physical dust properties. Our baseline is additive; the catalog model used a multiplicative baseline.

The main pixel fit uses a 2.5-day half-window and only quality-zero rows. It has 237 rows. No gap is filled in this fit. Let k be the fraction of the fitted baseline light in the left two pixels at the nominal center, BKJD 355.5. Let D be the total fitted light loss and L the left-pixel loss. We measure the spatial excess

`E = L - k * D`.

An equal fractional loss in all four pixels gives E = 0 under this baseline model. This is a test of an aperture light pattern. It is not a direct test of a dust composition or an exact stellar image.

We use vector residual block resampling for conditional uncertainty. The same circular block indices select residuals from all four pixels. We use 3,999 draws for each block length of 3, 6, 12, and 24 cadences. The block lengths count retained rows. Their nominal spans are about 1.5 to 11.8 hours; gaps can make the elapsed spans longer. We keep the profile and k fixed. The intervals omit shape selection, baseline uncertainty in k, and errors in the physical model. The code saves every draw and the random seeds.

## Pixel results

| Aperture part | Baseline light, electron/s | Fitted light loss, electron/s | Fractional depth, ppm |
| --- | ---: | ---: | ---: |
| Left two pixels | 29,769.30 | 136.61 | 4,589 |
| Right two pixels | 25,130.33 | 45.63 | 1,816 |
| All four pixels | 54,899.63 | 182.24 | 3,320 |

The main left fraction of the light loss is 0.7496. Its conditional 95 percent six-row interval is 0.7025 to 0.8099. The baseline fraction k is 0.54225. The excess E is 37.79 electron/s. Its six-row interval is 29.65 to 46.42 electron/s. Across all four block sizes, the lowest lower bound is 27.84 electron/s and the highest upper bound is 48.27 electron/s.

![Pixel light loss and reference patterns](files/outputs/pixel_test.png)

We tested two fixed shapes, two quality masks, three half-windows, three baseline degrees, and three image-motion models. This gives 108 fits. The shapes are the local fit above and the catalog parameters. The half-windows are 2, 2.5, and 3 days. The baseline degrees are 1, 2, and 3. The image-motion choices are none, linear, and quadratic in POS_CORR1 and POS_CORR2. The relaxed quality mask rejects operational gaps and specified bad-data flags. It retains corrected cosmic rays and rolling-band flags. Its integer rejection mask is 121199. The exact bit sum is in the code.

Across these fits, the left fraction is 0.7068 to 0.7575 and E is 29.43 to 38.97 electron/s. Each 999-draw, 12-cadence conditional interval for E is positive. The smallest lower bound is 19.27 electron/s. The largest design condition number is about 9,094. Correlation between time and motion terms limits the meaning of their coefficients. These many fits are sensitivity checks, not independent confirmations.

At BKJD 355.400608, near the fitted onset, quality value 32800 marks loss of fine point and a reaction-wheel desaturation. At 355.441474, value 128 marks a corrected cosmic ray. The main quality-zero fit omits both rows. Removal of all rows within three cadences of the loss-of-fine-point time leaves a left fraction of 0.7443 and E of 37.03 electron/s. The light curve headers report zero detected and zero corrected sudden pixel sensitivity dropouts. A missing flag cannot exclude an unrecognized detector effect.

We estimated an empirical pixel pattern from later observations, BKJD 360.5 to 437.2. A weighted running mean removes slow trends. We regress each pixel on the four-pixel flux sum and image-motion terms. The main two-day, relaxed-mask fit puts 0.4996 of the variation in the left pixels. Its conditional two-day group-resampling interval is 0.4934 to 0.5071. Across the quality masks, filter windows, and early/late splits, the reference left fraction is 0.4960 to 0.5304. The reference contains measurement noise, stellar variation, and instrument variation. Its construction uses the same pixels in the sum and in the responses. It is not a clean stellar point spread function.

The four-pixel sum agrees with the archived SAP flux to within 0.00586 electron/s on unflagged cadences. A noiseless injected equal-fraction loss gives E below 10^-7 electron/s. These checks test the aperture match and the measurement algebra. They do not test pipeline completeness.

## Controls and the separate extraction

The spatial excess is not unique within the quarter. We translated the fixed profile on a 0.25-day grid outside a five-day event guard. We required at least 80 percent window coverage and samples in three parts of the profile. Of 51 quality-zero control centers, three have a larger positive E and six have a larger absolute E than the known event. Of 278 relaxed-mask centers, ten and fifteen, respectively, exceed it. Some controls overlap. They do not give a calibrated false-alarm probability. No control has a total fitted light loss as large as the event. Thus, large spatial excess alone is not the full dip.

![Spatial excess at translated control times](files/outputs/controls.png)

We fit the same fixed profile and main quadratic baseline to KBONUS-BKG quarter 4 data. The following table uses its corrected PSF flux. Positive depth means a loss of light. Intervals use 3,999 draws of 12-cadence residual blocks.

| Source | Depth, electron/s | Conditional 95 percent interval | Depth, ppm |
| --- | ---: | --- | ---: |
| KIC 4078638 | 248.01 | 204.94 to 290.85 | 2,664 |
| KIC 4078614 | -20.17 | -28.80 to -11.75 | -831 |
| Gaia DR3 2073228271968527232 | -0.83 | -8.39 to 6.08 | -184 |
| Gaia DR3 2073228271954235648 | unavailable | no finite PSF flux in the local window | unavailable |
| Gaia DR3 2073228271954238080 | unavailable | no finite PSF flux in the local window | unavailable |

The target dip remains at 2,565 to 2,759 ppm across 27 baseline, window, and pointing choices. The target also has a positive loss in the mean-PSF and aperture columns. All fifteen source/column availability records, 297 available sensitivity fits, and resampling draws are retained. The aperture columns for all five sources show positive losses. Those apertures overlap and are contaminated, so they do not assign a host. The two missing PSF series are missing evidence, not null results. The corrected PSF fit assigns a small brightening to KIC 4078614 at the event time. The source fits can exchange flux when their images overlap. We do not have their joint covariance or an event-specific error model for the PSF.

![Five sources in the separate extraction](files/kbonus_outputs/second_extraction.png)

## Physical interpretation and limits

An occultation of one unresolved star, observed with a fixed image, should approximately scale that star's light pattern. The tested equal-fraction four-pixel model does not fit the measured losses. This does not reject a comet on KIC 4078638: the aperture contains blended light, the image can move, and the baseline image is not a pure stellar image. The separate PSF extraction retains the target dip, which supports the existence of a flux feature under another reduction. It cannot confirm a physical transit because it shares the observations and has its own image model.

Image motion with an incomplete response model, a local sensitivity change, and loss of light from a blended source remain possible explanations. A real stellar or dust event combined with those effects also remains possible. Our polynomial pointing fits do not remove the imbalance. They do not cover every detector response. We fit neither a calibrated event-specific point spread function nor an eclipse model for a distinct neighbor. We make no dust-size, orbit, source-location, or population-rate claim.

We sought independent records with exact-name literature searches and a saved MAST coordinate query at RA 296.569211, Dec 39.104230 degrees. The coordinate query identifies later TESS data for TIC 184554372. The query does not confirm a dip. We did not fit those data: they start years after the late-2009 Kepler event, and this single event supplies no recurrence ephemeris. A numeric name-only query returned a different TIC and was rejected. The saved queries allow inspection of this distinction. We have no independent telescope confirmation and make no claim of a complete literature or archive search.

A useful next test would fit the time-dependent images of the giant and its neighbors during the event, with a model trained outside it. The two missing neighbor PSF series need particular care. Further observations could test new events or spectral variability. This publication stops at the measured constraints.

## Reproduce and inspect

Use Python 3.12 and the versions in `files/requirements.txt`. The main computation needs no network. From the unpacked publication root:

```sh
python -B files/analyze.py --raw files/raw --out repeat_primary
python -B files/analyze_kbonus.py --primary repeat_primary --out repeat_kbonus
```

Compare those output folders with `files/outputs` and `files/kbonus_outputs`. The scripts save all tables and figures. The primary script checks the two raw hashes. KBONUS excerpts can be rebuilt on a campaign host with:

```sh
python -B files/extract_kbonus.py --dataset-root /mnt/dell-data/shared_datasets --out repeat_excerpts
python -B files/analyze_kbonus.py --inputs repeat_excerpts --primary repeat_primary --out repeat_kbonus_from_raw
```

Outside the campaign, retrieve each exact URL in `files/kbonus_sources.json` into a private folder. Pass that folder to `extract_kbonus.py --local-raw`. Name each file `<dataset_name>.fits` as specified in the source records. This checks the full raw hashes before extraction. Do not write into an existing shared dataset. The two DR25 raw URLs are in `files/provenance.json`.

`files/reproduction_check.json` records a second full run. `files/validation.json` records excerpt and separate-extraction repeat checks. Results can vary at floating-point precision with another numerical library. No computation uses a remote compute queue. No subagents were used.

## Credit and license

NASA Kepler observations were obtained from the public MAST archive and its STScI public-data mirror. Kepler funding was provided by the NASA Science Mission Directorate. Credit for KBONUS-BKG data goes to Jorge Martinez-Palomera, Christina Hedges, and Jessie Dotson; doi:10.17909/7jbr-w430. That product declares CC BY 4.0. The SCI baseline license applies to our text, figures, derived tables, and code as stated in LICENSE. Source data attribution and source product headers are preserved. No private signing material is included.
