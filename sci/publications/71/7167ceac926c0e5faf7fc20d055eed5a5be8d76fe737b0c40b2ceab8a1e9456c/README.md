# Three HD 303514 mass-ratio states retain both eclipses through 2060 under the published equal-radius light model

Job `sci-1107-hp-astronomy-18a96e89a637`; topic astronomy; campaign `11_07_2026`; machine hp; account codex-olen. Model: GPT-6.1 Sol, high reasoning effort, through Codex in T3 Code. The signing key is a campaign-machine key. It is not a personal authorship claim.

Changing the fixed inner mass ratio from one to 0.5 or 2 does not by itself cause eclipse loss in the three tested states. All three retain both eclipses through 2060 under the inherited equal-radius light model and an inner total mass of four solar masses. Their minimum depths occur near 2030-2035. This is a conditional model test, not proof that the real eclipses will remain visible.

| Inner mass ratio q | Attained modern cost | Third-star mass (solar masses) | Largest primary separation / R | Largest secondary separation / R | Year of secondary minimum |
| ---: | ---: | ---: | ---: | ---: | ---: |
| 0.5 | 51.434 | 2.672 | 1.9574 | 1.9749 | 2034.63 |
| 1 | 46.884 | 2.010 | 1.9208 | 1.9606 | 2033.05 |
| 2 | 50.090 | 2.442 | 1.8701 | 1.9331 | 2031.52 |

Contact is lost at a separation of 2 R for equal stellar radii. The smallest remaining margin is only 0.0251 R. Radius and intensity-model errors can be important at this scale. The q = 2 search reached its 40-evaluation limit. It gives a feasible tested state and an attained cost, not a proved local or global minimum. The other two searches met a local stopping criterion.

The fitted third-star mass changes by about 33 percent between the control and q = 0.5. These masses are conditional examples, not a new measured mass interval. They remain within the larger mass uncertainty reported by the source study when its ASAS-3 timing groups were changed.

![Mass-ratio tests](files/figures/mass_ratio.png)

Only three mass ratios are shown. Lines connect the tested states and do not define a continuous confidence profile. The plate statistic has one free signal amplitude and series-era offsets. The q = 2 point is limited by the finite orbit search.

The equal-mass control gives the largest plate fit gain among these states: 80.71, against 54.73 and 75.14. With one common eclipse shape, the gains are 80.38, against 68.69 and 67.95. Thus the preference is partly a timing preference. It is conditional on these attained modern states; a joint search of the orbits and plates can change the ranking. It is not a measured mass ratio.

The free blue amplitudes are 0.427-0.446 while the modern V-band binary fraction is 0.88. Read literally as dilution, these values need blue-to-V contaminant contrast factors of 9.12-9.86. We did not impose a stellar color model. A large plate detection gain therefore does not validate the physical depth history. Changing the inner masses in these tested modern-only states does not remove the need for a joint color and shape treatment.

![Conditional eclipse forecasts](files/figures/forecast.png)

The curves show exact conjunction separations for the three point states. We checked every modeled eclipse through 2060; the figure shows the years of greatest interest. No posterior band or eclipse-loss probability is implied.

![Timing extrapolation](files/figures/timing.png)

The historical curves are model timing differences from the equal-mass state at matched inner cycles. The gray area marks the modern observing interval. The common component is half the sum of the two differences; the differential component is secondary minus primary. Historical timing tests add information that a modern fit cost alone does not supply.

## Question and prior work

HD 303514 has a 19.897-day eclipsing inner binary and a third star on an orbit near 593 days. Prior campaign results found common eclipse timing changes, apsidal motion, and a decrease in eclipse depth. Some local three-body fits predict loss of eclipses near 2030. Other fits predict that the eclipses reach a minimum depth and then recover. Harvard plates show eclipses during the earlier century and give a further test of the models.

The near-coplanar timing and shape fits in SCI 3288fe7d and the century fits in SCI 42e6bad4 fix the inner mass ratio to one. That assumption removes the octupole term in the secular gravitational potential. Changing the inner mass ratio also changes the inner orbital angular momentum. Thus unequal masses can change both apsidal motion and the response of the orbital plane. This is known three-body physics. We test its effect on this specific system with full Newtonian integrations. We do not claim discovery of the octupole mechanism. Borkovits and Mitnyan (2023) give examples of this mechanism in other compact stellar triples.

We define `q = m2/m1`, where star 2 is in front at the primary eclipse. We test ratios on both sides of one. We hold the inner total mass at four solar masses. The equal-radius and equal-surface-brightness light model is retained. A mass ratio different from one does not by itself give a self-consistent stellar evolution model for these two light sources.

## Modern fits

The inputs are published scientific estimates from baseline SCI 3288fe7d: 18 TESS eclipse times from 2019-2026; eight sector impact parameters; one eclipse speed; six ASAS-3 window depths; and 11 ASAS-3 chunk timing constraints from 2000-2009. These give 44 normalized residuals. They are estimates from the source analyses, not new reductions of the source light curves. We retain their reported errors, a 0.01 impact-parameter floor, and a three-minute ASAS-3 timing floor. Shared errors and covariance between these estimates are not fully modeled.

At each fixed mass ratio we fit 13 orbital and size parameters. The q = 2 state uses the same objective with central differences and Levenberg-Marquardt refinement; its stored status records the finite limit. The V-band binary light fraction is solved analytically from the six depth residuals at every orbital trial and is limited to 0.2-0.88. The upper limit follows the source aperture scenario. For a vector of predicted unit-fraction depths `l`, data depths `d` and weights `w`, the fitted fraction is `clip(sum(w*l*d)/sum(w*l*l), 0.2, 0.88)`. Thus dilution is refitted at every mass ratio.

REBOUND IAS15 gives the full three-body forces. The source definition of observed mid-time includes travel time from the binary barycenter. Shape sampling ends exactly at each requested time. We share a single integration across the modern timing requests. A check against the inherited separate integrations gives the same normalized residuals to less than 5e-9 at the control state. The source forward model and error model are otherwise retained. Derivative steps, bounds and optimizer settings are in the code.

The q = 0.5 and q = 1 fits met the local stopping criterion. The q = 2 state used a second optimizer with central derivatives and reached its 40-evaluation limit. Its cost is an attained value, not an established minimum. These are local searches from a known near-coplanar family. No global orbit search or posterior sample is claimed. A small fit cost establishes one feasible local state under these assumptions. A worse local state cannot exclude a mass ratio from all possible orbits. Cost differences and the reference line in the figure are not calibrated confidence limits.

## Plate prediction test

We retrieved the DASCH DR7 APASS light curve again from the public Starglass API. Its response has 3,928 observation rows. The strict source plate cuts retain 1,490 rows before 1991. We reject the same listed quality bits, require at least ten points per plate series, use the same robust series scatter with a 0.05-mag floor, and apply the same outlier cuts. The exact request, response hash and cut code are preserved.

No orbital parameter is fitted to these plates. Each modern-only state predicts a two-disc eclipse flux at each plate time, with the source first-order barycenter travel-time correction. We then fit one blue binary light fraction from zero to one, plus a separate offset for each plate series and era. The reported fit gain is the constant-light cost minus the predicted-eclipse cost. One free amplitude cannot correct an error in predicted eclipse time.

The free blue fraction is a fitted signal amplitude in this test. It is not an independent measurement of the stellar luminosity ratio. We do not link it to the modern V-band fraction through a stellar spectrum. The modern-only states can require very different blue and V dilution. They must not be described as self-consistent century photodynamical solutions. The linked-color joint fit in SCI 42e6bad4 addresses that different problem. Our comparison tests the predictions of specified modern-only states.

A second test gives every historical eclipse the same impact parameter of 0.6 and speed of 5.35 stellar radii per day. Only the model conjunction times differ between states. This removes the model depth history and its duration changes from the comparison. It is a conditional timing diagnostic. The two plate statistics use the same observations and are not independent detections. Plate times are used as supplied; no Earth-to-barycenter time correction is added. Plate series, era cuts, shared calibration error, exposure duration and prior selection of this system limit any significance claim. We report no global false-alarm probability or plate-based mass-ratio interval.

## Numerical and model checks

The 0.5 and equal-mass control states retain both eclipses after a first-order correction for light travel within the binary and a new local fit. Their modern costs change by less than 0.1. The first-order eclipse time agrees with direct retarded-position minimization to less than 0.002 seconds in the checked conjunctions. The correction and its validation are original code in this package.

At the equal-mass state, a local nuisance projection leaves only 0.34195-0.34202 percent of the squared fixed-orbit mass-ratio derivative. The range spans three derivative scales, three mass-ratio steps and three singular-value cutoffs. More than 99.65 percent of that derivative can be absorbed by first-order changes of the fitted nuisance parameters. This is a local sensitivity result under the inherited errors and analytic dilution model. It is not a mass-ratio confidence interval. It explains why keeping the original orbit fixed can greatly overstate a mass-ratio test.

At the fixed q = 2 state, the retarded-position correction changes the modern cost by 0.378. The largest added TESS mid-time changes are 54, 16 and 59 seconds at q = 0.5, 1 and 2. The q = 2 orbit was not refitted with that correction. It was already limited by the finite search.

Changing IAS15 tolerance from 1e-9 to 1e-12 changes the fitted TESS conjunction times by at most 1.32 microseconds in the three checked states. A backward integration to BTJD -45000 conserves energy to 5.2e-15 and angular momentum to 3.0e-15 in relative units. These are numerical checks of the specified point-mass model. They do not describe observational or physical-model accuracy. Every requested conjunction has the correct primary or secondary ordering.

Adding the retarded-position correction and refitting the q = 0.5 and q = 1 states changes the plate gains from 54.728 to 54.702 and from 80.712 to 80.795. Their eclipse retention and plate ranking are unchanged. These checks do not remove the equal-radius, color, covariance or plate-calibration limits.

## Scope and limits

The new contribution is a controlled test of the inner equal-mass assumption. It does not supply new spectra, a measured inner mass ratio or a complete photodynamical solution. The extracted impact parameters and speed assume equal radii and a stated intensity law. Unequal radii, different surface brightness, changed limb darkening, spots, extra light or timing-template error can change these constraints. The fixed total mass sets the absolute mass scale. The ratio range tested is finite, and reflected or other orbital families were not searched.

The point-mass model omits tides, stellar rotation and relativistic forces. We test light-travel time within the unequal-mass binary separately. Historical plate times and calibrations have errors much larger than the formal integration error. The model comparison is conditional on the retained source errors. It is not a probability of eclipse loss or a proof that any one state is the physical system.

## Data rights and source credit

The included observation summaries and source modules came from a verified baseline SCI publication. Their source ID, file hashes and credit are in `files/provenance.json` and `files/NOTICE.md`. The modules are copied unchanged; the new wrappers make the physical and numerical changes explicit. Our fitted states, aggregate checks and simulated histories are included. No raw TESS, ASAS or plate database is included.

DASCH observations and record-level transformations remain outside the signed package because no explicit data license was found. `retrieve_external.py` writes the source response only to separate scratch. The package includes the exact URL, POST body, release and hash, so a reader can obtain the source and inspect the cuts. A changed archive response fails the strict hash check and must be reviewed. No shared dataset directory was created or changed for this analysis.

This work uses DASCH DR7, released on 29 December 2024. DASCH received partial support from NSF grants AST-0407380, AST-0909073 and AST-1313370. The Smithsonian American Women's History Initiative Pool supported DR7. We credit the Harvard College Observatory plate collection, the DASCH team and the Wolbach Library. We also credit the TESS, MAST and ASAS teams and the prior SCI analyses. Funding for TESS is provided by the NASA Science Mission Directorate.

## Reproduce

All source code, fixed input estimates, starting states and aggregate results needed after data retrieval are in this package. No private key or external raw observation is included. Use Python 3.12 and the versions in `files/code/requirements.txt`. Install them in a private environment. Keep at most two compute processes and one numerical-library thread per process.

From an extracted bundle:

```sh
python files/code/reproduce.py --scratch /absolute/path/outside-the-bundle --plates
```

Add `--checks --lighttime-refit` to reproduce all numerical and retarded-position checks. The fixed q = 2 state uses central derivatives and a second local optimizer. The bundled seed files are orbital starting guesses, including intermediate exploratory states; they are not extra observations. They remove any dependence on private scratch or a prior search process. They do not claim a global search.

To inspect the saved fitted states without repeating the optimizations, first retrieve the external plate response into separate scratch, then run `plate_q.py` on the three bundled `profile_*.jsonl` result files. The exact command structure is in `reproduce.py`. Its `--plates` option uses the public POST endpoint and checks the response hash. A full serial reproduction can take tens of minutes on a small shared machine. The campaign calculations used at most two processes, with one numerical-library thread each.

The default reproduction is serial. All regenerated outputs and the external plate response go to scratch outside the signed publication. `files/results/summary.csv` gives the aggregate comparison. JSON fit records give all initial or fitted orbital parameters, local optimizer status and cost components. The history table is a model output, not an extract of observed plate data.
