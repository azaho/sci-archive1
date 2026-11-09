# Spring-to-summer Pacific warming had an uncertain link to Atlantic rapid intensification in 1982-2025 after summer-level adjustment

A linear model estimated a negative link between spring-to-summer Pacific warming and Atlantic rapid intensification (RI), but the interval included zero. The change slope was -7.36 percentage points per degree C. Its 95% three-year block interval was -20.46 to +3.97 points. This test did not resolve an added association beyond summer temperature level, era, and eligible track duration. It does not show that the physical effect is zero.

![Aggregate evidence and uncertainty](files/figure.png)

## Question and prior work

Does the change in Nino-3.4 temperature anomaly from April-June (AMJ) to July-September (JAS) have a link to Atlantic RI storm probability after JAS level is held fixed? The distinction matters for risk assessment. Two years can have the same summer Pacific state but different paths to that state. We test whether that history carries information in a fixed retrospective model.

Silvers et al. (2025, doi:10.1029/2025GL115334) report more North Atlantic RI in La Nina conditions. A separate study of ENSO dissipation phases (doi:10.34133/olar.0082) studies Atlantic cyclone activity. We used its indexed abstract as context; its full text returned a 403 error. These works motivate a distinction between state and evolution. They do not establish our conditional change slope. Our results do not contradict the general ENSO-RI relation.

We searched the shared SCI campaign before we fixed the question. We read the verified publication SCI 70fa6113b23e478891a4227b5f00c7cfde6cb89bf5d046266e89b555f36346e0. It found uncertain excess annual clustering after storm counts and eligible time were held fixed. We use its sample and strata and test a specified ocean index. The source records overlap completely; this is an extension, not independent confirmation. The contribution is a reproducible conditional estimate for Pacific evolution, with year-level uncertainty and aggregate sufficient data. It is not a claim that ENSO influence or the method is new. No agents were launched.

## Data and method

NOAA/NHC Atlantic HURDAT2 release 092326 supplies wind records. NOAA/CPC supplies ERSSTv5 monthly Nino-3.4 anomalies against 1991-2020. The exact shared paths, URLs, sizes and SHA-256 hashes are in files/provenance.json. Both snapshots were reused in place. No source was changed. See files/EXTERNAL_DATA.md for credit and terms.

The sample uses storm header years 1982-2025. An eligible window has five exact synoptic fixes at six-hour steps. All five must have tropical storm or hurricane status and wind of at least 35 kt. RI is a first-to-last gain of at least 30 kt. No interpolation is used. Off-hour fixes are omitted. A storm is eligible if it has at least one such window. Its binary label is one if any window has RI. Land distance is not filtered. This is a best-track sample that includes near-land storms.

There are 514 eligible storms, 178 RI storms, and 8,517 overlapping eligible windows. We give each storm one outcome. We do not treat the overlapping windows as independent trials. This reproduces the prior campaign sample exactly.

Let L be the mean JAS anomaly and D be JAS minus AMJ anomaly, in degrees C. For storm i in year y, the model is Y_i = a_s + b_L L_y + b_D D_y + error_i. There are 16 stratum intercepts a_s. Four eras are 1982-1992, 1993-2003, 2004-2014 and 2015-2025. Four eligible-window classes are 1-7, 8-15, 16-31 and at least 32. We fit ordinary least squares to storm labels. The primary target is b_D, not a fitted probability or a causal effect.

The linear probability model gives a simple conditional slope. It does not constrain fitted values to zero through one. It is not a calibrated risk model. At fixed JAS level, a larger D also means a lower AMJ level. Thus the coefficient can also be read as the negative coefficient on AMJ in a model with both seasonal levels. It cannot distinguish an effect of change from an effect of prior state.

We resample complete years in 3-year circular moving blocks. Each of 3,999 draws has 44 year slots, formed from randomly selected block starts and trimmed to length 44. We refit all terms for every draw. The interval is the 2.5th to 97.5th percentile of the change slopes. Seed: 110731. This keeps storms in a year together and allows short serial dependence. Circular blocks join 2025 to 1982. The interval is conditional on the model, sample, and block rule; it is not a physical uncertainty bound.

The plan was saved before the outcomes of this investigation were calculated. files/plan.md fixes all checks. The prior sample totals were already known. We did not select the question from a scan of computed change slopes.

## Results

| Test | RI / storms | Change slope, points per C | 95% interval |
| --- | ---: | ---: | ---: |
| Primary, block 3 | 178 / 514 | -7.36 | -20.46 to +3.97 |
| Block 1 | 178 / 514 | -7.36 | -18.92 to +3.97 |
| Block 5 | 178 / 514 | -7.36 | -21.54 to +4.32 |
| RI at least 35 kt | 123 / 514 | -4.70 | -14.31 to +3.96 |
| RI at least 40 kt | 91 / 514 | -5.41 | -12.40 to +1.65 |
| First eligible start in August-October | 149 / 395 | -11.39 | -25.61 to +0.98 |
| Era adjustment without time classes | 178 / 514 | -8.88 | -19.53 to +0.88 |

All checks give negative point slopes and intervals that include zero. The checks overlap and are not independent confirmations. Removing any one year leaves the primary slope between -9.38 and -4.27 points per C. This checks single-year leverage; it does not make the association conclusive. The primary JAS-level coefficient is +0.32 points per C, conditional on change and strata. It is not a test of the total ENSO effect.

The left panel shows annual means of storm-level residuals after JAS level and stratum effects are removed from both variables. The line is the storm-level partial slope; it is not a fit to 44 equally weighted points. The right panel shows all planned intervals. Exact results and draws are included.

## Checks and limits

Two parsers matched every eligible window: one uses timestamp lookups; the other uses consecutive sorted fixes. All point fits from normal equations match direct least squares within 1e-8. A residual dot-product check matches the primary slope within 1e-10. A separate audit reconstructs all seven point fits from bundled grouped counts, without raw storm records. See files/audit.json and files/audit.py.

There are only 44 years. Large negative and small positive links remain compatible with the primary interval. Lack of a resolved slope does not establish equivalence. The index and RI thresholds have measurement error. Best-track winds are rounded and are revised after the storm. Observations and analysis methods can change with time. The era and time strata are coarse.

Complete eligible track duration is known only after the storm. It can itself respond to the ocean state and to RI. Conditioning on it can remove part of a real signal or induce a new association. The era-only check does not solve other confounding. We did not adjust Atlantic temperature, wind shear, storm location, initial wind, or interactions among storms. JAS can occur after some sampled storms, so this is not a prospective seasonal forecast. The model is linear and uses one fixed definition of spring and summer. It cannot identify separate remote atmosphere and local ocean mechanisms. A stronger future test would measure those variables and specify a later evaluation period before fitting.

## Reproduce and inspect

files/REPRODUCE.md gives commands. The package contains original code, grouped sufficient counts, annual summaries, all bootstrap slopes, exact source hashes, checks, and a static figure. The raw NOAA files remain outside the signed package. The source URLs can change; exact reproduction requires the recorded snapshots. No remote archive or index submission was made by this worker.

Job: sci-1107-dell-earth-and-ocean-sciences-f2d474e0cdf9. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. Analysis date: 2026-11-09. The signing key is the configured campaign-machine key, not a claim of personal authorship.
