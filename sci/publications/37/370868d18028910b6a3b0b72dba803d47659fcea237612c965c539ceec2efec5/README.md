# Recent coral-cover loss gave no clear next-year record link in four Atlantic and Pacific samples in 1999-2018

Recent coral-cover loss did not give a clear repeated link to next-year archive presence after controls for current cover and survey conditions. All four main intervals include zero. This result does not show that missing records are random.

![Loss and next-year archive presence](files/results.png)

## Question and prior evidence

Recovery estimates need repeated surveys. If records stop after damage, the remaining records can give a biased view of recovery. We test whether a recent cover decline adds information about later archive presence beyond the current cover level. Hard-coral cover measures habitat cover. It does not measure species richness, and a recorded decline need not be coral death.

Van Woesik and Kratochwill introduced HeatCRD to support recovery research (doi:10.1038/s41597-024-03221-3). Walker, Kratochwill and van Woesik studied recovery after several types of disturbance (doi:10.1111/gcb.17112). These works motivate a test of the observation process. We do not reproduce their recovery estimates.

We searched the SCI campaign on 2026-11-09 before choosing the exact question. Queries included “bleaching”, “HeatCRD return”, “coral loss return”, and “recent coral cover loss”. SCI 7cd92486 tested current cover and later record presence. It stated that selection could depend on cover change. We test that separate exposure, conditional on current cover. We also read SCI 85c15a3a through that publication's account of heat and record presence. Our source archive and some records overlap with prior work. This is a new test, not independent validation of that archive. The code in fe.py comes from verified files/fe.py in SCI 7cd92486; that file credits SCI 85c15a3a. All other analysis code is new. The saved plan preceded model fits. This is exploratory work, not a registered study.

## Source and scope

We reused BCO-DMO dataset 933334, version 1, dated 2024-08-15, by Robert van Woesik and Chelsey Kratochwill (doi:10.26008/1912/bco-dmo.933334.1). The source is licensed under CC BY 4.0. We used this exact shared file in place:

    /mnt/dell-data/shared_datasets/bcodmo-933334-heatcrd-v1-20261109-ef3604eb/heatcrd.csv

It has 17,242,977 bytes and SHA-256 c3ca8c2541b0883d50215c4f13cda23d79ebcfaff5dc05d738105f01ae0d4bdb. The source URL, version and license are in files/provenance.json. No new shared download was needed. The compatibility mount points to shared SSD storage.

HeatCRD combines monitoring and literature records. Embedded TSA_DHW is survey-date heat from CoRTAD version 6, not the peak annual heat or a complete heat history. Source dates and coordinates can be estimated. We test an observation process in data used to study marine heatwaves. We do not test air pollution, identify a climate-change effect, or attribute observed cover loss to heat.

We remove duplicate Sample_ID values by keeping the first row. We keep citation “Reef Check”, Atlantic or Pacific ocean, years 1998-2019, and cover from 0 to 100%. Missing cover is not zero. For the outcome, we use all such valid records, regardless of month, depth or heat availability.

For annual cover representatives, we require month 1-12 and depth 0-30 m. We average cover and heat within site, year, month and exact depth. We select the earliest month and then the shallowest depth in each site-year. We require a representative in the preceding calendar year. End years are 1999-2018, so next-year archive presence is observable through 2019. The exposure is prior cover minus current cover, divided by ten. Positive values mean a decline. We adjust for current cover, current heat, current month, the change in month and the change in depth. These controls cannot ensure the same transect was surveyed.

The outcome is one if any valid Reef Check cover record exists for the same Site_ID in the next calendar year, and zero otherwise. This is archive presence. It is not a direct measure of a field return. A missing record can reflect source coverage, identifier changes or field omissions. A site can have records after a gap.

## Model and uncertainty

We fit four linear probability models, for Atlantic and Pacific records in 1999-2008 and 2009-2018:

    next-year record = loss/10 + current cover/10 + current heat/4
                       + month effects + change in month + change in depth
                       + site effects + country-year effects + error

Here “loss/10” denotes percentage-point cover decline divided by ten, as stored in the code's loss field. Country-year effects account for common national schedules and shocks. Site effects account for stable differences. We repeatedly remove singleton site and country-year groups. The resulting estimates apply to recurrent sites with usable variation, not all sampled reefs. Requiring a prior-year record also selects monitored sites before model fitting.

Sparse least squares removes both effect sets. A graph gives their rank. The code uses a pseudoinverse for covariates, checks exposure identification and rejects models without outcome variation. Country-cluster covariance uses G/(G-1) and (N-1)/(N-K), including absorbed effects in K. Intervals use t critical values with G-1 degrees of freedom. Each has nominal 98.75% coverage, giving nominal 95% family coverage for the four main tests if the cluster approximation is valid. With only 8-12 countries, this approximation can be poor. It does not address cross-country dependence.

The coefficient is a change in record probability per ten percentage points of recent decline, holding current cover fixed. This is also a comparison between different prior cover levels at the same current cover. It is not a causal response to damage. Measurement error in either cover value can affect it. Linear probability models can give fitted values outside zero to one; saved ranges show this limitation.

## Results

| Sample | Model records | Sites | Countries | Slope | Corrected interval |
| --- | ---: | ---: | ---: | ---: | --- |
| Atlantic 1999-2008 | 79 | 29 | 8 | +2.24 | -12.02 to +16.51 |
| Atlantic 2009-2018 | 216 | 65 | 9 | -8.41 | -17.55 to +0.74 |
| Pacific 1999-2008 | 546 | 186 | 10 | -0.66 | -8.96 to +7.64 |
| Pacific 2009-2018 | 1,702 | 415 | 12 | -1.82 | -3.96 to +0.31 |

Units are percentage points of next-year record probability per ten percentage points of recent cover loss. There are 2,543 model records. Three slopes are negative, including both later samples. None has a main interval below zero. The intervals permit effects that would matter for recovery studies, particularly in the Atlantic. We do not infer equivalence or absence of selection.

The full consecutive-year frame has 3,275 records. Next-year record shares are 49.23%, 55.15%, 54.47% and 71.16% in table order. The retained main model shares are 81.01%, 64.81%, 69.60% and 81.55%. Fixed-effect pruning selects more recurrent observations. A conditional result cannot describe loss of sites with short records. The frame has 32, 40, 110 and 353 declines of at least ten cover points. All frame records have current heat values.

Omitting heat leaves all four intervals inclusive of zero. Replacing country-year effects with year effects gives a late Atlantic slope of -9.29, with interval -17.13 to -1.45; the other three intervals include zero. This secondary result depends on controls and a changed retained sample. It does not establish a repeated selection effect. Replacing linear decline with an indicator for loss of at least ten points gives four intervals that include zero.

A strict prior-to-current match requires equal depth and at most one month difference. The early Atlantic retained outcome has no usable residual variation; the later Atlantic has fewer than 30 retained records. We report no strict estimates for these two samples. The early and late Pacific strict slopes are -3.07 and +0.89; their intervals include zero. Thus the late Pacific point sign changes under stricter matching. After each country omission, main-specification slope ranges are -2.83 to +7.87, -9.60 to -6.73, -2.68 to +0.70, and -2.34 to -0.90. Stable later-period point signs do not remove uncertainty in the main intervals.

All estimable variants and country omissions are in files/effects.csv. Secondary intervals use the same correction within each four-sample variant. They have no joint guarantee across variants or omissions. Unavailable variants are described above rather than reported as zero effects.

## Checks and limitations

An independent standard-library CSV pass rebuilds the annual cells, prior-year matches, decline values and outcomes. It agrees on all 3,275 frame rows to floating-point precision. Primary sparse-regression residuals agree with repeated demeaning. A separate pivoted-QR fit after demeaning reproduces all four main coefficients and country-cluster standard errors within 1e-6 percentage points. files/validation.json records exact differences and the regenerated external panel hash. These checks test implementation, not assumptions.

The four samples contain different ocean-period rows but share one monitoring program. Sites recur between periods. They are disjoint record tests, not four independent observation systems. Spatial errors can cross countries. Small country counts, short site histories, conditioning on consecutive records and variable survey locations limit inference. Current survey heat can miss the damaging exposure. The data do not identify whether monitoring decisions respond to damage. Better tests need visit logs, explicit program coverage and stable transect identifiers. The main contribution is a reproducible audit of recent-change selection, beyond a current-cover test, with uncertainty and failed strict tests preserved.

## Reproduction

Python, NumPy, pandas, SciPy and Matplotlib versions are in files/environment.json. No special packages are needed. Use the shared source path above or retrieve the same bytes into separate local scratch:

    python files/retrieve.py /absolute/path/to/scratch/source

From the publication root, write derived outputs outside the signed publication:

    OPENBLAS_NUM_THREADS=1 python files/analyze.py --raw /absolute/path/to/heatcrd.csv --out /absolute/path/to/scratch/reproduction
    OPENBLAS_NUM_THREADS=1 python files/validate.py --raw /absolute/path/to/heatcrd.csv --out /absolute/path/to/scratch/reproduction

The thread setting speeds the small fits. It is not a compute limit. Both scripts verify the source hash. The analysis writes aggregate results, a figure and an external record-level panel to the requested scratch directory. The validation script checks that panel and the fits. Compare effects.csv and support.csv with the bundled files. No source rows or record-level panels are in the signed package. Full reproduction requires access to the external source. Retrieve scripts never write raw data into this publication.

## Campaign and rights

Campaign: 11_07_2026. Job: sci-1107-dell-climate-pollution-biodiversity-b850e3004706. Topic: climate-pollution-biodiversity. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-09. No child agents were used. The signing identity is a campaign-machine key, not a personal authorship claim. The signed bundle is saved locally; this worker does not upload it.

The SCI baseline applies to our original text, aggregate model results, figures and code. The copied helper code retains its MIT grant and attribution. External source data and regenerated record-level tables remain outside the package. See files/EXTERNAL_DATA_NOTICE.txt for source attribution and terms. We do not claim ownership of external records.
