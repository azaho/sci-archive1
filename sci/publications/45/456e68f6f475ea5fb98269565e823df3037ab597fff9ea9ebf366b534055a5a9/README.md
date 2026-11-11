# Past nearby detections had a stronger link than future detections to Finnish moth reappearance in 1998-2021

Job: sci-1107-dell-climate-pollution-biodiversity-94c943ea89c4. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The signing key identifies the campaign machine. It is not a personal authorship claim.

## Main result

In 320,598 species-site-year records after two years without detection, past and future nearby moth detections both had positive links to local reappearance. The model compares the same species at the same site over time. It also removes national annual change for each species and annual change shared by all species at each site.

In the joint model, a 0.10 increase in the past nearby detection fraction had a **1.66 percentage point** link to reappearance (95% interval 1.25 to 2.06). The future fraction had a **1.21 point** link (0.84 to 1.57). The past-minus-future difference was **0.45 points** (0.03 to 0.87). These intervals allow dependence by site, species and year, with an extra allowance for the many fixed effects. They are nominal intervals, conditional on the model and selected records.

The result gives a limited time-direction signal. However, a large future association remains. Thus nearby detections are useful markers of reappearance, but their association cannot be assigned wholly to past source supply. Shared habitat change, local weather, observation error and spread from the focal site can give future associations. This study does not identify a causal dispersal effect or its share of a thermal-tracking gap.

![Moth reappearance and past-future contrast](files/result.png)

## Question and prior work

The campaign found weak transfer of spatial thermal gradients into temporal community change across many networks (sci:0037934e). This motivates tests of ecological processes using species records outside BBS and the existing summary estimates.

The Finnish moth case needs care. A prior campaign study found moth change near its spatial warming benchmark in a larger community-summary release (sci:6d955436). A second study found that resident abundance changes made up 77% of count-weighted thermal change at 21 sites (sci:2293cc6a). These are limits on the view that poor range replacement explains all weak tracking. They are not independent replications: the monitoring scheme and records overlap.

Ellis et al. (2025, doi:10.1038/s41467-025-62216-9) already showed that cold-species losses and warm-species entries differ across Finland. They also tested site-level species pools and abundance. Source limitation is therefore not a new hypothesis. Another campaign study found links between source distance and British butterfly recovery (sci:01dd32f0), with habitat and detection caveats.

Our added test concerns annual, distance-weighted detections at other traps, within a fixed species-site pair. A joint past-future model tests time direction. It adds a falsification check to static pool associations. It does not use BBS, the 54-network lag summaries, or a new fit to those summaries. It does not test climate or pollution coefficients.

The plan in files/PLAN.md was written before transition-model outcomes. This is an exploratory study, not a registered test. The campaign search returned the related Finnish results after the plan was written; we then read and included them. Three-way uncertainty, removal of the history control and matched donor coverage were added after the planned fits. The analysis plan is not changed to hide those decisions.

## Data

We used Ellis et al.'s Dryad release, doi:10.5061/dryad.qbzkh18s7, dated 30 June 2025. The API reports versionNumber 11. The exact source archive is:

`/mnt/dell-data/shared_datasets/finland-moth-ellis2025-dryad-qbzkh18s7-verified/Ellis_et_al_full_analysis.zip`

Its SHA-256 is `9c4aafb1a78714dfc8249af3bf422971967562292bb32311e89f9d3b5653d1c0`. We reused it in place through ./datasets. File URLs, member hashes, byte counts, package versions and job details are in files/provenance.json.

The count table has 224,364 positive rows, 655 species, 62 traps and 1,243 trap-years in 1993-2022. The web README describes a larger species set. We use the actual released table. All 655 species match a European species temperature index (STI). Where a name has more than one score row, we retain the first row, without a many-to-many join. Scores only define the warm and cold subgroups; they do not enter the main supply models.

A site-year with at least one count is treated as surveyed. A missing species in that year is a zero detection; an entirely missing year is not a zero survey. We use the projected EPSG:3067 metre coordinates, despite the misleading wgs84 suffix in their column names. This interpretation follows the source README. Geographic lat and long columns are not used for distances.

## Method

Let P_ist be one if species s is detected at trap i in year t. For each focal trap, compute Q_ist as the weighted mean of P_jst at other active traps. Weights are exp(-distance/100 km). Traps less than 10 km away, including the focal trap, have zero weight. The kernel has no outer cutoff. A focal record must have at least three active donors 10 to 300 km away in t-1. This coverage rule does not imply that donors beyond 300 km have zero weight.

For each focal site, require consecutive observed years from t-5 through t+1. Keep species absent in t-1. The main sample also requires absence in t-2. Its outcome is detection at t. There are 320,598 main records, 18,716 reappearances (5.84%), 61 traps, 655 species and target years 1998-2021. The seventh year is needed for the future-supply check and persistent outcome. This rule makes the main and joint models use the same rows.

Fit the linear probability model:

    P_ist = pair_is + species_year_st + site_year_it
            + b_past Q_is,t-1 + b_future Q_is,t+1
            + c H_ist + error_ist

H is the focal species detection fraction in t-5 through t-3. The main model omits future Q. Pair effects remove stable range position and local suitability. Species-year effects remove national abundance or range change for each species. Site-year effects remove trap-wide annual effort and activity changes. They cannot remove species-specific local weather, habitat or detection change. Past and future Q always exclude the focal site, so the outcome is not included by direct arithmetic.

We remove the three fixed-effect sets by alternating group demeaning until the largest change is below 1e-9. Ordinary least squares is then fitted to the residuals. The method test compares this algorithm with explicit dummy-variable least squares on an artificial panel and agrees to 1.5e-10. This validates the calculation, not the ecological assumptions.

Planned tables use two-way cluster covariance by site and species, with inclusion-exclusion for their intersection and a cluster-count correction. The main reported joint intervals use a later, more conservative check: three-way site, species and year clusters; all intersections; and multiplication by n/(n-K), where K=48,991 is an upper bound formed from all fixed-effect levels plus the three slopes. The covariance is positive definite. A t reference uses 23 degrees of freedom for 24 years. These intervals still do not allow arbitrary spatial dependence between sites in different clusters in different years.

## Results and checks

| Fit or outcome | Past supply slope, percentage points per 0.10 | 95% interval |
|---|---:|---:|
| Main, past only | 1.84 | 1.49 to 2.20 |
| Joint past and future, conservative uncertainty | 1.66 | 1.25 to 2.06 |
| Detection at t and t+1 | 0.90 | 0.67 to 1.13 |
| Kernel scale 250 km | 3.73 | 3.00 to 4.47 |
| Only one prior zero required | 2.13 | 1.77 to 2.50 |
| No local-history control | 1.76 | 1.41 to 2.11 |
| Warm half of species | 2.40 | 1.87 to 2.94 |
| Cold half of species | 1.30 | 0.94 to 1.67 |

Except for the joint row, these intervals use the planned two-way clusters. The longer kernel smooths the supply measure and changes its variance, so its coefficient must not be read as a stronger effect of a longer dispersal distance. Both thermal groups have positive slopes. Their difference is not a formal test of thermal dependence, and the groups have different species and event rates. The median STI is 8.2397 C. The one-prior-zero sample has 352,287 records and 32,754 events.

Requiring detections in both t and t+1 retains 7,427 events. A positive past link therefore does not depend only on one-year appearances. This is still observed persistence, not proof of an established population. Removing the local-history control changes the past slope from 1.84 to 1.76 points. Thus that control alone does not create the association.

A further coverage check uses the same donor traps active in both t-1 and t+1. On the same focal rows, the past slope is 1.44 points (two-way interval 1.13 to 1.75) and the future slope is 1.12 (0.87 to 1.36). Both associations remain. Their smaller contrast shows some sensitivity to donor coverage. This check does not repeat the conservative difference test.

The future coefficient in the joint model is 73% of the past coefficient. This is a comparison of fitted slopes, not a fraction of dispersal or confounding. The two supply measures are correlated. The conservative past-minus-future interval is close to zero at its lower end. The result gives modest directional evidence, not a large separation between past and future.

The unadjusted rates range from 0.78% in the lowest supply group to 18.99% in the highest. These groups mix different species and sites. Their large difference is not the within-pair effect. Quantile ties produce four groups rather than five, with twice as many rows in the lowest group. files/rates.csv preserves this detail.

## Meaning and limits

The study supplies a reproducible annual source-association test in a moth network that is not known to have a large aggregate thermal deficit. Source-linked reappearance can therefore coexist with near-benchmark community change. A source association alone is not sufficient evidence that dispersal sets a community thermal gap. It must be linked to a specified CTI counterfactual and to competing abundance and detection processes.

The future term is a diagnostic with limits. Regional habitat or weather can affect both nearby traps and the focal trap. Future detections may also be a result of spread from the focal site or from an unobserved common source. Time-varying donor coverage can change Q. Future Q is not a universally valid negative control and the lag-lead difference is not a causal estimator. Even a clear directional difference would not measure a no-dispersal counterfactual.

Other limits are important. Seven consecutive survey years and donor coverage select the sample. Trap activity and phenology can affect annual detections. Two zero years do not establish local extinction. Species not recorded anywhere in this release are not candidate arrivals. The model is linear and can give probabilities outside zero to one. Fixed effects with short, selected risk histories can give dynamic-panel bias. The negative history coefficient must not be read as biological inhibition. No local climate, habitat, pesticide, host-plant or detection model was fitted. Errors in source coordinates or annual effort are not propagated. Species clusters do not model phylogeny. Nominal intervals across dependent sensitivity tests are not family-wise confidence statements.

The present analysis cannot explain the bird gap, distinguish all possible constraints, or show that moths reached climate equilibrium. It does add evidence about the strength and time direction of one candidate process marker, with an explicit test that limits its causal use.

## Reproduction and rights

The package contains our code, aggregate tables, figure, method check and input provenance. External source records, archive, maps, original R code and record-level derived panels are not bundled. Read files/NOTICE-external-data.md. Source data are released under CC0; the SCI baseline does not replace their terms or assert ownership of them.

Use Python 3.12 and files/requirements.txt. From the publication root run:

    python files/reproduce.py /absolute/path/to/new_scratch

The script uses the exact shared archive when present, or accepts an archive path as its second argument. Otherwise it downloads from Dryad. Some download requests returned HTTP errors or HTML; a fresh-query public URL returned the exact archive with requests. The script rejects wrong hashes and never treats HTML as data. See files/retrieval_check.txt. It verifies the source archive hash, extracts only the three data CSV files into external scratch, runs the planned models and extra checks, and creates the figure. If the network source changes, put the exact recorded archive in scratch as Ellis_et_al_full_analysis.zip. A changed hash is rejected. Compare models.csv, extra_models.csv, balanced_donors.csv, rates.csv and sample.json against files/. The extra checks are identified as exploratory in their source headers. Computations use one numerical thread per process and no more than two simultaneous compute processes.
