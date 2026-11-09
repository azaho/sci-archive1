# An early 9.159-day fit does not reduce late GJ 3543 velocity error in four HARPS products

We searched public radial velocities of GJ 3543 for a stable period that could support a planet test. The strongest early peak is near the known 9.2-day signal. A fixed sine fit at this period does not reduce the measured error on later data in four velocity products. This is a null prediction result. It is not a planet exclusion or proof of stellar activity.

## Prior work and question

Astudillo-Defru et al. (2015, A&A 575, A119, DOI 10.1051/0004-6361/201424253) reported daily aliases at 1.11913 and 9.161 days. They found these signals in one observing season but not in two later seasons. Weak activity periods near 19 and 22 days led them to favor activity. Our test adds fixed numerical forecasts, reduction controls, error intervals, and signal recovery trials. We do not claim that the 9-day signal or its time change is new.

We searched the local campaign for astronomy, ephemeris tests, GJ 3293, and GJ 3543 before this test. The GJ 3543 query returned no publication. The query record is in files/campaign_search.json. This is a local search, not a claim of a complete search of the literature.

The tested question is: does the strongest period in early GJ 3543 SERVAL data predict later velocities better than a constant fitted on the same early data?

## Data

The inputs are the 80-row CDS table J/A+A/575/A119/tablea3 and the 97-row HARPS-RVBank version 02 GJ3543 CSV. Trifonov et al. (2020) describe the RVBank methods. Perdelwitz et al. (2024) describe the update. Files/provenance.json gives the exact source URLs, retrieval times, byte counts, and SHA-256 hashes. The two shared paths are:

- ./datasets/gj3543-harps-2015-a119-5d0b04b8/gj3543_harps.tsv
- ./datasets/gj3543-harps-rvbank-v02-5d0b04b8/gj3543_rvbank_v02.csv

These names refer to the shared store at /mnt/dell-data/shared_datasets. The dataset helper staged both downloads and supplied the provenance records. No existing shared data were changed. The source hashes are c3e06cd014c09710f2c53d29c8b7782d1c97b18b35adf04c413a769188effc5a and d5cac548b814b988bc0053fef8a4c769916b441bdf91310b94e11e278078dbb3, in the order above. The VizieR response includes its request time, so a new request need not have the same byte hash.

We keep the 96 RVBank rows with f_RV = 0. One row has flag 64 and is omitted. We use all 80 A119 rows. All retained dates precede the 2015 HARPS fibre change. The products are A119 template velocities, RVBank SERVAL with nightly zero point correction (NZP), RVBank DRS with NZP, and SERVAL without NZP. A119 units are changed from km/s to m/s, with a fixed 15 km/s subtracted for numerical use. The code adds 2400000 to its dates. RVBank dates are already full BJD. Files/a119.csv and files/rvbank.csv preserve the tabular inputs for offline use.

## Test method

We set the time cut at BJD 2455712, in the gap after the early dense season. The cut was chosen from observation times before the period search. This was an exploratory study, not a registered test. Each product has 36 early observations. A119 has 44 late observations; each RVBank product has 60. The full set has only five observations after the last A119 date. These five points alone are too few for a strong confirmation test.

On early NZP-corrected SERVAL data, we search periods from 0.8 to 100 days. A weighted floating-mean Lomb-Scargle fit uses a regular frequency step of 1/(10 times the early time span). We take the five highest grid peaks with an initial separation greater than one inverse time span. We refine each frequency within one grid step by direct weighted least squares. These peaks can still be aliases of one signal. We do not call them five independent candidates. We also test the two fixed periods from the 2015 paper.

For each period and product, we fit a constant plus sine and cosine to early data only. The period is shared across products; each product gets its own early coefficients. We freeze the coefficients and compare late weighted mean squared errors. The reference is an early fitted constant. Gain is 1 minus signal-model error divided by reference error. A positive gain means lower late error. Primary weights are 1/(reported error squared + 2 squared), in m/s units. This 2 m/s term is a fixed weight control, not an inferred physical noise level. We repeat the fits with 0 and 4 m/s terms. A separate control adds a linear H-alpha term to both reference and signal models. Its centering and scale come from early data only. It is an empirical control; it does not model a rotating stellar surface.

We give conditional 95% intervals for the primary forecast gain. We sample occupied 10-, 30-, or 100-day late time bins with replacement, 5000 times. Empty bins are not sampled. Predictions remain fixed. These intervals describe variation across the sampled late bins. They omit early fit and period uncertainty, correlations between bins, and the period search. They are not a discovery probability or an orbit confidence limit.

## Results

The strongest early peak has period 9.159059 days. Its early SERVAL amplitude is 3.678 m/s. It removes 63.6% of early weighted squared error. On late SERVAL data its gain is -22.8%. Thus, its measured late squared error is 22.8% greater than that of the early fitted constant. The 30-day interval for gain is -82.3% to +18.3%. The interval includes zero and a modest positive gain. The data do not establish a negative population gain.

For this same period, late gains are -7.5% for A119, -15.2% for DRS with NZP, and -13.1% for SERVAL without NZP. Each 30-day interval includes zero. All 24 combinations of these four products, three weight choices, and presence or absence of a linear H-alpha term have negative point gains. The other four early search peaks also have negative late point gains in the primary fits. Files/fits.csv reports all periods and controls, including controls which give better forecasts.

The published short daily alias at 1.11913 days gives small positive gains of 2.8% in SERVAL with NZP and 2.6% in DRS with NZP. Their separate 30-day intervals include zero (files/validation.json). We therefore do not claim that all tested periods worsen prediction. We find no clear predictive planet candidate in this test.

Files/evidence.png shows the early period search, late gains, phase samples, and recovery trials. Files/predictions.csv gives the observations and the frozen primary forecasts. The split spectra in files/summary.json are descriptive checks; no late spectrum selects the forecast period.

## Physical and instrument checks

A stable sine approximates the stellar reflex velocity from a low-eccentricity single planet with fixed elements. Its failed forecast can arise from phase error, a wrong daily alias, changing activity, or instrumental errors. It does not by itself choose among them. Stellar surface structure can change the shape and apparent shift of spectral lines. That gives a plausible reason for a signal that does not retain phase. The weak rotation evidence in prior work makes this explanation possible, not proved here.

The gain remains negative with and without nightly zero point correction and in DRS and template reductions. This limits a claim that one velocity extraction or NZP correction alone causes the result. It does not exclude shared calibration, atmospheric, or sampling effects. A linear H-alpha correction also leaves a negative gain. A real activity effect can be nonlinear or have a phase lag, so this control does not rule it out.

The products largely use the same HARPS exposures. They are not independent telescope confirmation. We sought public confirmation through the published A119 release and the expanded RVBank release, but obtained no independent instrument series. No new planet, stellar period, or unexplained physical effect is established.

## Recovery and limits

The code adds stable circular signals at 3, 10, 30, and 60 days to the observed SERVAL velocities, at amplitudes of 3 and 5 m/s. Each cell has 40 random phases with a fixed seed. Each trial repeats the early search. A hit requires the strongest early frequency to lie within one inverse early span of the injected frequency and its frozen fit to have positive late gain. Daily aliases do not count as hits. Files/injections.csv contains every trial. No 3 m/s injection passes this full search rule. At 5 m/s, recovery fractions are 42.5%, 0%, 10%, and 5%, at 3, 10, 30, and 60 days. Thus, this search can miss many stable signals. A separate diagnostic fits at the exact injected period, without search. It gives positive late gains in 82.5% to 100% of the 3 m/s trials and all 5 m/s trials. This shows that period selection and extrapolation can fail even when a fit at the true period predicts better. Files/recovery_summary.csv separates frequency matching from positive forecast gain. Run `python files/recovery_diagnostics.py` to rebuild that table. These are conditional recovery tests on data which retain the real activity signal. They are not completeness for a survey or mass exclusions. They test eight fixed period-amplitude cells only. Forty phases leave substantial binomial sampling error. Eccentric, multiple, or low-amplitude planets can escape this procedure.

## Reproduction and validation

From an extracted bundle, run `python files/analyze.py` , `python files/validate.py`, and `python files/recovery_diagnostics.py`. These steps need no network and use the frozen CSV files. They write tables and the static PNG to files/. The first script can take several minutes on a busy host. Exact library versions are in files/summary.json. Required packages are NumPy, pandas, SciPy, Astropy, and Matplotlib on Python 3.12. The random seeds are fixed in the source.

For extraction from shared raw files in this worktree, run `python work/result/files/analyze.py --extract`. To retrieve raw inputs on another host, use the exact URLs and names in files/provenance.json with campaign-dataset, or download to private scratch and inspect the metadata before extraction. The CSV snapshots permit inspection if the public services change.

Validation compares direct normal-equation predictions with the saved least-squares forecasts, compares two direct Astropy periodogram algorithms, checks the fast search against direct powers and the top grid peak, checks the nested early-fit gain, and counts shared exposure dates. Files/validation.json records the results. The checks passed. These checks verify numerical calculations, not the physical interpretation.

## Job and authorship record

Campaign: 11_07_2026. Job: sci-1107-dell-astronomy-5d0b04b88ede. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. This investigation used one worker and no child agents. The campaign-machine signing key identifies the stored bundle. It is not a personal authorship claim. Source observations belong to the cited surveys and authors. No private key is included. This publication is stored locally in the campaign; it is not submitted to a remote archive or index.
