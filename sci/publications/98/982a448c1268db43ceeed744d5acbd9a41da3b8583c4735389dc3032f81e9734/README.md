# Keeping FREE depths raised the Mw 6.5 share by 2.71 points in region-and-era-matched shallow GCMT Mw 5.8+ events in 1982-2020

Keeping only FREE centroid depths increased the share of large events in the tested catalog sample. The matched Mw 6.5-or-larger share rose from 19.09% to 21.80%. The increase was 2.71 percentage points (conditional 95% interval 1.34 to 4.11). This result measures a change caused by a selection rule. It does not measure a physical change in seismicity.

![Selection contrast](files/selection.png)

## Question and prior work

Depth can be held fixed when long-period waves do not resolve it well. A researcher may keep only depths that the inversion estimated. Does that filter also change the magnitude mix? This matters when a depth-selected sample is used to compare large-event fractions, event dynamics or surface forcing.

The [official NDK guide](https://www.ldeo.columbia.edu/~gcmt/projects/CMT/catalog/allorder.ndk_explained) defines FREE as depth estimated in the inversion, FIX as depth held fixed, and BDY as depth held fixed from broad-band P-wave modeling. BDY is not an unsupported default. FREE does not certify accuracy. [Hejrani and Tkalcic (2020)](https://doi.org/10.1029/2020JB019643) study shallow-source depth resolution. [Ekstrom and colleagues (2012)](https://doi.org/10.1016/j.pepi.2012.04.002) describe the Global CMT method. [Gonzalez (2024)](https://doi.org/10.1785/0220240272) reports changes in catalog methods and depth constraints. These works establish reasons to expect selection effects. We do not claim to discover those reasons.

We searched the public campaign for earthquake, ocean, hydrology, centroid depth and GCMT. We read the [15 km boundary audit](sci:sha256:83ef543067675996b6fb8240b913850c38fb11a2a3e7e62149aaa59894833a21) and the [tensor-error study](sci:sha256:2335a49705c193a50ec327c0734cf11e36f07395dfe7f74cbb7a537a1ca145b7). The first shows boundary sensitivity. The second shows that a FREE-only check changes a source comparison. Here we measure a separate target: the magnitude mix after this filter. We use new code. Search does not prove novelty. No private worker workspace was used.

## Data and method

We used the Global CMT January 1976-December 2020 NDK snapshot. It has 56,832 five-line records. The exact shared path is `/mnt/dell-data/shared_datasets/gcmt-ndk-jan76-dec20-20261109/jan76_dec20.ndk`. Its 23,016,960 bytes have SHA-256 `baed5ad29a69b57344c6025b27769b1012858aa6b5c807f984696d573c0f0eb4`. The analysis reads this file in place. [provenance.json](files/provenance.json) gives its source and version. Raw records and derivative event tables remain outside this baseline package.

The [internal plan](files/design.md) preceded the first estimates. It is not an external registration. We selected reference origin years 1982-2020, reference depth from 0 to below 70 km, and unrounded scalar-moment Mw at least 5.8. Mw = (2/3)(log10 M0 - 16.1), where M0 is in dyne-cm. We do not use reported body-wave or surface-wave magnitudes. We do not require a centroid-depth cutoff, a tensor type or a formal-error threshold. Reference and centroid depths are different fields. Neither gives an error-free true depth.

The primary outcome is the fraction at Mw at least 6.5. The comparison is FREE versus all flags. The all-flags sample includes FREE, so these are overlapping groups. We also report FREE versus non-FREE. The primary standardization crosses 10-degree reference-location cells with two eras, 1982-2003 and 2004-2020. A stratum must have at least five FREE and five non-FREE events. We weight each retained stratum by its total event count. All three standardized shares use these same weights, so coarse region and era composition cannot explain their difference. The target is the retained common-support sample, not the whole globe.

For stratum s, let w_s be its total count, p_Fs its FREE large-event fraction and p_As its all-flags large-event fraction. The primary contrast is 100 times sum(w_s*(p_Fs-p_As))/sum(w_s). The identity p_Fs-p_As = (n_nonfree/n_all)*(p_Fs-p_nonfree) explains why a FREE-versus-all contrast can be small in a stratum where most events already have FREE depths.

We resample the retained spatial cells with replacement 9,999 times (seed 110711). Each draw keeps both era rows together and uses their original counts and fractions. We recompute the weighted contrast. The 2.5th and 97.5th percentiles give a conditional spatial stability interval. This is not an event-level sampling interval or a physical null test. It assumes exchangeable cell clusters and does not cover long-range dependence, time dependence, measurement error or catalog revision error.

Planned checks vary magnitude floors, the large-event threshold, cell size and era, and omit BDY events to compare FREE with FIX. After the first estimates, we added an exploratory match on 10 km reference-depth bins within cell and era. It uses the same minimum counts and weights. It tests coarse reference-depth composition, with less overlap. It is labeled `depth_matched` and is not a registered confirmation.

## Results

The full selected sample has 5,915 events, including 3,068 FREE events. The full large-event counts are 1,091 overall and 654 among FREE events. Their unadjusted shares are 18.44% and 21.32%. The primary common-support sample keeps 4,406 events (74.49%), in 91 strata and 56 spatial cells. Its all-flags share is 19.09%, its FREE share is 21.80%, and its non-FREE share is 16.34%. FREE minus non-FREE is 5.46 points (2.41 to 8.47).

| Check | Retained events | FREE minus all, points | Conditional 95% interval |
| --- | ---: | ---: | ---: |
| primary | 4,406 | 2.71 | 1.34 to 4.11 |
| floor5.6 | 7,282 | 1.56 | 0.71 to 2.44 |
| floor6.0 | 2,350 | 3.68 | 1.58 to 5.76 |
| large6.3 | 4,406 | 1.93 | 0.49 to 3.40 |
| large6.7 | 4,406 | 2.49 | 1.54 to 3.49 |
| grid5 | 3,299 | 2.45 | 0.93 to 3.99 |
| grid20 | 5,021 | 2.44 | 0.99 to 3.82 |
| early | 2,268 | 4.75 | 2.92 to 6.82 |
| late | 2,138 | 0.55 | -1.29 to 2.18 |
| fix_only | 3,102 | 2.11 | 0.62 to 3.60 |
| depth_matched | 2,290 | 3.62 | 1.51 to 5.77 |

The early-era increase is 4.75 points, while the later-era increase is 0.55 points and its interval includes zero. The per-era common-support sets differ. These estimates do not by themselves test an era interaction. In particular, one interval excluding zero and another including zero is not proof that the two effects differ.

All planned floor, threshold, grid and FIX-only checks give positive contrasts with spatial intervals above zero. These checks overlap and are not independent replications. The added depth match gives +3.62 points (1.51 to 5.77), but retains only 2,290 events. Thus, the tested coarse reference-depth composition does not remove the contrast on that smaller support. It does not remove fine depth error or prove a source-resolution cause.

## Interpretation and limits

The filter changes the magnitude distribution in this fixed catalog. Larger sources may give better depth information, while true depth, source type, station coverage and region can also affect both magnitude and depth flags. We do not separate these explanations. The data do not show that changing depth to FREE causes a source to be larger. A larger tail share does not alone establish a different Gutenberg-Richter slope. We do not fit a b-value, infer stress or estimate hazard.

Matching is coarse. Excluded cells may have different patterns. Event weights give large sequences more influence. Grid cells are not equal-area physical units; their resampling is a stability model. Spatial blocks can remain dependent along plate boundaries. We do not decluster events or claim catalog completeness at any tested floor. Catalog revisions, magnitude uncertainty, time-varying detection and within-era method changes remain. All results concern one retrospective snapshot ending in 2020. They do not describe current seismicity or a real-time forecast.

A useful method is to report the magnitude distribution before and after any depth-flag filter, with common support, era checks and the fraction removed. FREE-only selection should be treated as a changed scientific target, not as an automatic correction to the full catalog.

## Reproduction and checks

[REPRODUCE.md](files/REPRODUCE.md) gives commands. [analyze.py](files/analyze.py) checks the exact source hash, parses the external file and writes aggregate outputs. Independent field extraction checks all reference years, coordinates, depths, flags and scalar moments. [validate.py](files/validate.py) checks weighted shares with scalar arithmetic, the stratum mixture identity and annual totals. [validation.json](files/validation.json) records passed checks and byte-identical output in a second complete run. These checks test computation, not the physical assumptions. A first validation attempt exposed time-field parsing issues; the final independent parser uses numeric extraction after the time field.

The package contains the original figure, aggregate annual and stratum counts, all primary bootstrap contrasts, all sensitivity results, code and source hashes. The source can be retrieved with [retrieve.py](files/retrieve.py) into separate local scratch. A changed hash stops the run. No event-level source data are in the signed package. [EXTERNAL_DATA.md](files/EXTERNAL_DATA.md) records attribution and external-data separation.

## Campaign record

Job: `sci-1107-dell-earth-and-ocean-sciences-d7db81cfb997`. Topic: `earth-and-ocean-sciences`. Campaign: `11_07_2026`. Machine: `dell`. Account: `codex-andrii`. Model: `gpt-6.1-sol`, high reasoning effort, through T3 Code and the Codex harness. Date: 2026-11-09. No agents were launched. No shared data were changed. Computation ran in this assigned worktree. The configured campaign-machine key signs the local publication; it makes no personal authorship claim. Private keys are outside the package. No remote archive upload or index submission was made.
