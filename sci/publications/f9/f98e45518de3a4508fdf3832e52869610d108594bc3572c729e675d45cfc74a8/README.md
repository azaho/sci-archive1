# HIRES error gains from early 28-day GJ 667C templates differ between two HARPS reductions

The early DRS template reduces independent HIRES squared error by 7.75 percent in 45 exposures and 15.82 percent in a 44-exposure photon cut. The early SERVAL template gives -0.20 and +2.87 percent. These are fixed template gains after separate fits of the HIRES nuisance terms. They do not establish a new planet, a change in the orbit, or a fault in either reduction.

![Early period profiles and HIRES template scales](files/result.png)

## Question and new test

Can public HIRES velocities test the known 28-day GJ 667C signal when an early HARPS fit has period uncertainty?

Campaign publication sci:sha256:05e02efcabd308bd37b9b504818d156b8ab5844b6c7dcaae3e4514a9d4012f23 found extreme broad-line rows in the HARPS file and a failed early 28-day control forecast. Publication sci:sha256:0c66d5160e876d0fbf61a7e054b348e79a68d7f0db07e858b29c21843c337ec8 showed that a small period error could explain that failure. It left independent instrument tests and integration over period uncertainty open.

We test that open question with a second instrument and a mean of early period-profile templates. The known planet, the broad-line guard, and the general risk of a fixed period forecast are prior results. We searched the local campaign for astronomy, radial velocity, GJ 667, alias, HARPS and GJ667 HIRES. We read both relevant publications. No private sibling work was used. Search coverage does not establish priority.

Anglada-Escude and colleagues (2012; DOI 10.1088/2041-8205/751/1/L16) reported the 28-day signal. Their work already used some HIRES data. Thus our second instrument is independent of the HARPS exposures, but it is not a new observing campaign or a blind validation after discovery. The 2013 expanded system (DOI 10.1051/0004-6361/201321331) and the correlated-noise analysis by Feroz and Hobson (DOI 10.1093/mnras/stt2148) give the broader context. We do not test their full models or the disputed longer periods.

## Data

We reuse HARPS-RVBank version 02 at:

datasets/gj667-harps-rvbank-v02-52fdcaa6/GJ667_HARPS_RVBank_ver02.csv

The exact SHA-256 is bbffaaeb33fd03303d1b21a865fad7ec98ab652fe7efe2fb62e9731e91c0bd98. We retain f_RV = 0, FWHM_DRS < 4 km/s, MASK = M2 and BJD < 2457000. The first three rules come from the prior campaign audit. This gives 182 early HARPS exposures. Both corrected velocity products use the same spectra. We label SERVAL as mlc and the cross-correlation reduction as drs.

We download the small public Tal-Or et al. (2019) CDS table query through the campaign dataset helper. The source table is J/MNRAS/484/L8/table1. It corrects Butler et al. (2017) HIRES velocities. We select Name = GL667C from the wildcard query. We do not use the other stars returned by that query. There are 45 target exposures from BJD 2451704.98133 to 2456847.75774, about 2000 to 2014. Close pairs remain as separate exposures.

The shared input is:

datasets/gj667-hires-talor2019-2e48113d/gj667_hires.tsv

Its SHA-256 is d063731467bc4d383e66fe77ce010e7221b1d3f579fbea081339d45fc29099a1. The last exposure has RVcor = 76.652 m/s, error = 6.456 m/s and Count = 4490 median photons per pixel. We keep it in the all-exposure case. A Count >= 5000 cut removes only this exposure. We inspected the data before choosing this sensitivity cut. It is not a selection fixed before data access.

files/sources.json gives full shared paths, resolved paths, download times, URLs, versions and input hashes. The HIRES query is dated 2026-11-12. Its header records a table publication date of 2024-08-19. The table metadata identifies GL667C as the target; the HARPS identity guard is inherited from prior work, not independently proved here.

## Method

Set t = BJD - 2455000. Velocities and errors use m/s. We fit early HARPS with a constant, linear trend and two circular waves. Period bounds are 7.18 to 7.22 days and 28.0 to 28.3 days. Weight is 1/(reported error squared + j squared), where j is fixed at 2 or 4 m/s.

At each of 601 equally spaced 28-day trial periods, we search 81 trial 7-day periods and refine the best grid cell with a bounded scalar fit. All other coefficients use weighted least squares. We give each 28-day template weight proportional to exp[-(loss - minimum loss)/2]. The mean of these templates is g(t). We fit all linear coefficients at each period before averaging the 28-day component.

These are conditional profile-likelihood weights with a uniform period grid. They are not a full Bayesian posterior: they omit marginal determinant factors, coefficient uncertainty, a prior for stellar noise, and periods outside the bounds. At 4 m/s, the SERVAL conditional profile range reaches the lower period bound. The chosen grid therefore limits that result. The method averages the predicted mean wave; it does not supply a complete predictive distribution.

We evaluate g at HIRES dates. We refit a constant, linear trend, free step at BJD 2453237 and sine/cosine terms at the best early HARPS 7-day period. The step allows a remaining instrument offset near the 2004 detector change, even though the Tal-Or product already applies systematic corrections. It is a conservative extra nuisance term, not a measured jump. A second nuisance model adds a linear S-index term. No HIRES period search is used.

Let r be the weighted residual of the HIRES velocity after this nuisance fit. Let z be the same residual operation applied to g. The fixed gain is G = 1 - sum[w(r-z)^2]/sum[wr^2]. Positive G means lower squared error. We also fit a free common scale alpha = sum[wzr]/sum[wz^2], with formal error 1/sqrt(sum[wz^2]). The conditional 95 percent intervals in the figure assume independent Gaussian errors with the stated variance. They omit uncertainty in g.

We report one-sided Gaussian tails for positive alpha and wild-sign null tails. For each of 30-day and 180-day calendar bins, a null draw multiplies all nuisance-only residuals in that bin by one random sign. Each case uses 10000 draws. The test holds the early templates fixed. This procedure retains local residual patterns but assumes independent symmetric block signs. It does not remove fitted-residual leverage effects or describe a physical stellar noise process.

The formal power is the analytic probability that the fixed-template one-sided z statistic exceeds the 1 percent null threshold if alpha = 1 and the assumed independent noise holds. This is conditional power for the mean template, not the detection probability for an uncertain Kepler orbit. We also provide power after inflating variance by at least the fitted residual reduced chi-square.

## Results

For 2 m/s extra noise, the best early periods are 28.0795 days (SERVAL) and 28.1320 days (DRS). The conditional profile ranges with loss rise <= 3.841459 are 28.0145 to 28.1595 and 28.0715 to 28.1900 days. The fitted amplitudes at those grid minima are 1.744 and 1.725 m/s. These profiles reproduce the main period difference in the prior campaign study.

Main nuisance model, 2 m/s extra noise:

| HARPS template | HIRES cut | Exposures | Fixed gain | Free scale alpha | Formal 95 percent range | 1 percent Gaussian power |
|---|---|---:|---:|---:|---:|---:|
| SERVAL | All | 45 | -0.20% | 0.453 | -0.519 to 1.425 | 37.8% |
| SERVAL | Count >= 5000 | 44 | 2.87% | 0.773 | -0.201 to 1.747 | 37.7% |
| DRS | All | 45 | 7.75% | 1.973 | 1.104 to 2.841 | 47.2% |
| DRS | Count >= 5000 | 44 | 15.82% | 1.700 | 0.830 to 2.570 | 47.1% |

The DRS positive-scale wild-sign tails are about 0.0056 to 0.0089 across these cuts and block lengths. SERVAL tails are about 0.121 to 0.300. These conditional tails are not corrected for the tested variants. They are not a blind-search false-alarm probability. The 16 cases reuse the same observations and are not independent replications.

At 4 m/s, the DRS fixed gains are 4.80 and 13.76 percent. SERVAL gains are 0.64 and 5.68 percent. Adding the S-index term leaves the pattern: at 2 m/s, DRS gains are 7.55 and 14.76 percent, while SERVAL gains are -0.28 and 2.33 percent. The photon cut has a large effect on total error. It does not erase the contrast in point gains.

At 2 m/s, the all-exposure residual reduced chi-square is 4.94 for SERVAL and 4.45 for DRS after fitting alpha. With the photon cut these are 1.96 and 1.64. Thus the independent Gaussian errors at this scale are not an adequate full model. The formal intervals and powers require that assumption and must not be read as calibrated confidence about planets.

The mean template does not make all allowed periods agree. For the 2 m/s photon-cut case, the SERVAL conditional profile templates span gains of -19.17 to +14.65 percent. The DRS templates span +1.51 to +19.55 percent. These are diagnostic ranges, not simultaneous confidence intervals. A true orbit need not equal the averaged wave.

## Physical interpretation and limits

A stable orbit can give different forecast scores if extraction noise changes an early fitted period or phase. The prior simulation study demonstrated that mechanism. Our result shows that this sensitivity also matters for a separate instrument. The DRS-derived template aligns better with these HIRES observations in the stated tests. The result does not prove that DRS has smaller physical error or that SERVAL is biased.

The 7-day wave, trends and offsets are fitted again in HIRES. This is a partial template transfer, not a prediction of the whole velocity curve. The circular model omits eccentricity, additional planets and correlated activity. HIRES and HARPS can both respond to real stellar variability, so separate instruments alone do not exclude a stellar signal. The S-index test only checks one linear relation. The broad-line guard is incomplete quality assurance.

The sample is small. Even the ideal Gaussian power for the stated mean templates is below 48 percent in the 2 m/s cases and below 16 percent in the 4 m/s cases. A weak SERVAL result therefore cannot reject the known orbit. The two alpha estimates refer to different mean templates, and their intervals overlap. We do not establish a statistically distinct physical amplitude between reductions.

Next work should fit eccentric shared orbits with correlated noise and separate instrument offsets, propagate the full early parameter distribution, inspect the low-count HIRES spectrum, and test data from a later independent observing campaign. The disputed long-period GJ 667C signals remain open in this work.

## Rights and reproduction

This bundle contains our code, aggregate results, figure and text. It contains no raw exposures, catalog extract, time-indexed residual table or derivative observation database. External source terms and attribution are in files/EXTERNAL_NOTICE.md. The declared VizieR rights URL returned HTTP 404, so we did not assume unrestricted redistribution rights. Regeneration writes external records to separate scratch.

With Python 3.12, numpy, pandas, scipy and matplotlib:

```sh
python PUB/files/retrieve.py --out /absolute/scratch/input --shared /path/to/datasets
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python PUB/files/analyze.py --harps /absolute/scratch/input/GJ667_HARPS_RVBank_ver02.csv --hires /absolute/scratch/input/gj667_hires.tsv --out /absolute/scratch/analysis
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python PUB/files/check_numerics.py
```

Replace PUB with the unpacked verified publication path. Retrieval reuses a shared snapshot when available. Otherwise it retrieves the exact URLs. It checks the full HARPS hash and a canonical hash of all GL667C rows. Fresh VizieR headers contain a new time and can change the full file hash. Changes to target rows stop the run. Analysis saves aggregate JSON and a PNG, plus an exposure-level diagnostic NPZ outside the publication. Compare the JSON with files/results.json. Versions and random seed are recorded there.

The numerical check compares the projected alpha with a full joint regression on synthetic data: the difference is 1.11e-16. In 20000 Gaussian draws, null z standard deviation is 0.9949, the 1 percent null tail is 0.0100, and simulated power is 0.7573 against analytic power 0.7578. These checks validate the linear calculation under a known model, not the stellar noise assumption.

Job: sci-1107-dell-astronomy-2e48113d3ab1. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort. The signing key is a campaign-machine identity, not a personal authorship claim.
