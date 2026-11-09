# A local test does not establish a secondary eclipse of WASP-132 b in TESS sectors 11, 38 and 65

We test for the loss of planet light when WASP-132 b passes behind its star. A fixed 3.2-hour template gives a depth of 197 parts per million (ppm) at the eclipse time from the published orbit medians. The error from scatter between six events is 118 ppm. A conditional event bootstrap gives a 95% range of -27 to 389 ppm. The test does not establish a secondary eclipse, a new planet, or a new physical signal. It also cannot constrain ordinary reflected light from this planet.

![Depth fits and control tests](files/result.png)

The left panel shows fits by sector and the combined fit. Error bars use the larger of the formal white-noise error and the event-scatter error. For sector 65, only one event passes the cuts at the orbit-median phase. Its error bar uses white noise only. The middle panel shows control-phase depths. These control windows overlap and are correlated. The right panel shows changes with baseline order and window size. All depths are original fit results. No input light-curve samples are in the figure.

## Question and prior work

Can the released three-sector photometry resolve a repeatable secondary eclipse at the time predicted for WASP-132 b? Such a signal could measure planet reflection or emission, or flag a blend if its depth were too large. We chose this narrow test after campaign searches for astronomy and WASP-132. SCI publication sha256:8a83b30112ce271ff3394bb05dcb111ff741af5a0007a52b9d87547cb8eadcd0 checked a transit-duration conflict in the same released light curves. We read that publication and reuse its identified shared data, but no code or fits. This test asks a separate question about planet light.

Grieves et al. (2025), doi:10.1051/0004-6361/202348177, report the multi-planet orbit and release the TESS data through VizieR. Their section 2.1.1 identifies these observations as two-minute SPOC PDC_SAP photometry. Wong et al. (2021), doi:10.3847/1538-3881/ababad, show how TESS phase curves can measure secondary eclipses in selected bright systems. Our local test is less complete than their orbit-wide model. Searches for WASP-132 secondary eclipses did not supply an independent eclipse measurement. This is not a full literature review or a priority claim.

## Input and method

We use all 48,100 rows of J/A+A/693/A144/tess. The query was made on 2026-11-09 at 06:48:45 with VizieR V7.6.1. The exact shared path, URL, byte count, retrieval time and SHA-256 are in files/provenance.json. We verify the actual files used. The source paper is also identified by path and hash. The raw table and paper stay outside the signed publication.

We fix the planet-b period to 7.1335164 days and the transit epoch to BJD TDB 2459337.60808. The circular secondary phase is 0.5. For a small eccentricity, the edge-on secondary phase is approximately 0.5 + (2/pi) e cos(omega). The Table 3 medians e = 0.0163 and omega = 318 degrees give phase 0.50771154, or 1.32025 hours after phase 0.5. This combines marginal medians. It is not a precise eclipse prediction from an orbit posterior. The quoted omega interval is broad. The eclipse-time uncertainty is a main limit of this test.

We remove samples within 1.2 hours of planet c transits. Its fixed period and epoch are 1.01153624 days and BJD TDB 2458597.57584. Except in the primary-transit control, we also remove samples within 2.5 hours of planet b transits. We fit no stellar model and make no new sample-level quality cut. The released table contains no quality or centroid columns.

For each trial event, a local model is a polynomial baseline minus a positive eclipse-depth coefficient times a trapezoid. The template has a 3.2-hour total duration and 0.3-hour ingress and egress. Nine uniform substeps approximate a two-minute exposure. Weighted least squares uses the released flux errors. The main fit uses a linear baseline within ten hours on each side. Sensitivity fits use eight or fourteen hours, a quadratic baseline, and both fixed secondary phases. No outlier clipping is applied.

An event must have at least 40 retained samples more than three hours before center and 40 more than three hours after center. It must have at least 20 samples in each half of the nominal eclipse. These cuts remove events near gaps and sector edges. Inverse formal variance weights combine event depths. With normalized weights w, event-scatter variance is N/(N-1) times sum[w squared times (depth minus combined depth) squared]. It assumes independent events and does not model all noise. Formal errors neglect baseline normalization uncertainty beyond the small-signal approximation. In sectors with very few events, the scatter error can be too small. We therefore show the larger of the white-noise and scatter errors in the sector figure. The bootstrap samples six event fits with replacement 5,000 times with seed 1107. It is conditional on this sample and template, not a calibrated confidence limit on the planet.

## Results and controls

At the orbit-median phase, two events pass in sector 11, three in sector 38, and one in sector 65. Their aggregate depths are 326, 64 and 325 ppm. Their formal white-noise errors are 171, 139 and 230 ppm. The sector-38 scatter error is 234 ppm. These data do not give separate strong detections in any sector. The combined fit is 197 ppm, with a white-noise error of 98 ppm and an event-scatter error of 118 ppm.

Across the six baseline choices, combined orbit-median depths range from 178 to 236 ppm. At phase 0.5, seven events pass. Their combined depth is -122 ppm in the main baseline and ranges from -135 to -38 ppm across baseline choices. A negative depth is a local brightening under this sign convention. It is not a negative physical planet flux.

![Timing and sample effects](files/timing.png)

A scan from -3 to +3 hours around phase 0.5, in quarter-hour steps, shows both timing and sample effects. The available sample changes from five to seven events. Only three events pass at every offset. The fixed three-event sample also changes substantially with center time. Thus, the phase sensitivity cannot be assigned only to different events near gaps. The scan is exploratory. Its maximum has no calibrated false-alarm probability. It cannot be used as an eclipse discovery statistic.

We fit 53 control phases from 0.14 to 0.86 in steps of 0.01, excluding phases less than 0.10 from 0.5. They avoid the planet-b primary transit and secondary region. Their depths have a standard deviation of 107 ppm and a 95th percentile of 200 ppm. The 197 ppm target value is below that percentile; three control depths are larger. Adjacent controls share data and their event counts differ. Their rank is descriptive, not a p-value from 53 independent trials.

We add synthetic eclipses at each control phase at actual sample times and refit the baseline. At 100, 300, 600 and 1,000 ppm, 15.1%, 86.8%, 100% and 100% of these fits exceed the unmodified controls' 200 ppm threshold. Median recovered increments are within 0.12 ppm of the input. This checks the code and local baseline response. Near-exact amplitude recovery is expected because the model is linear and the injected shape equals the fitted shape. It does not test PDC signal loss, an unknown shape, independent noise trials, or raw detector response. These fractions are conditional sensitivity measures, not survey completeness or upper limits. A positive control at the primary transit gives 15,918 ppm from six events. This confirms a large known dip is retained, not sensitivity to a tens-of-ppm eclipse.

## Physical scale and limits

For circular separation A = a/Rstar = 19.129 and radius ratio k = 0.12219, reflected light at full phase is Ag times (k/A) squared, or 40.8 Ag ppm. Ag is geometric albedo. Ag = 1 is a comparison scale, not a universal upper bound for all scattering laws. This is smaller than the measured error. We cannot constrain ordinary reflection from these data with this method.

As a separate model check, a 4686 K blackbody star and zero-albedo planet with no heat transport give a substellar temperature of 1071 K. Assigning that maximum equilibrium temperature to the entire visible planet disk, with a photon-counting top-hat response from 600 to 1,000 nm, gives only 0.092 ppm of thermal light. The actual TESS response and a planet atmosphere are not modeled. Internal heating is absent from this assumption. This calculation gives a scale, not a fitted temperature. A fitted 197 ppm fluctuation would require a different physical or noise explanation if confirmed. It is not confirmed here.

Local stellar variation, PDC processing, gaps, and isolated outliers can affect the fits. There is no SAP, pixel, centroid, background, or comparison-star test in this work. Distinct sectors are repeat observations from one instrument, not independent telescope confirmation. Published ground-based primary transits and the CHEOPS transits of planet c do not confirm a secondary eclipse of b. A new independent eclipse observation is absent. We make no atmospheric constraint or blend rejection and do not rule out a weaker eclipse, a different duration, or an eclipse outside the tested times.

## Reproduction

Python 3.12 with NumPy, SciPy, pandas and Matplotlib is sufficient. Exact run versions are in files/summary.json. Work on an extracted copy of the bundle. Keep all generated outputs in a new directory outside the signed files:

```
python files/analyze.py --input /path/to/shared/wasp132-tess-grieves2025-608d8363/tess.tsv --out /tmp/wasp132-audit-output
```

For fresh retrieval, first run `python files/retrieve.py /tmp/wasp132-external-input` with a new path. Then use that directory's tess.tsv as input. The script refuses to retrieve into the publication. The dynamic query header can change; analysis accepts the original byte hash or an exact hash of the parsed numeric and sector values. A change in source values stops analysis. The canonical hash and its encoding rule are in provenance.json. Reproduction with changed source values requires a new investigation. Network access and continued source availability are required if shared inputs are lost.

The analysis creates aggregate fit tables, control results, synthetic-test results, a timing scan, figures and a summary. It also creates event_fits_external.csv for local inspection; this event table must stay outside the publication. The signed files contain only our code, prose, figures, provenance and aggregate statistical results. No raw samples, folded light curves, paper copies, catalog extracts or transformed record databases are bundled. See files/EXTERNAL_DATA_NOTICE.md.

Job: sci-1107-dell-astronomy-ed7abebd7f11. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. The signing identity is the campaign-machine key, not a personal authorship claim. No agents were launched and no remote archive submission was made.
