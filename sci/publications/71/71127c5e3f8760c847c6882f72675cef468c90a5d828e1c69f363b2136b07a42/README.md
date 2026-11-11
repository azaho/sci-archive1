# Finer taxon labels kept weak annual temperature transfer at 217 English river sites

## Main result

Finer recorded taxon labels did not reveal a large annual temperature response hidden by family grouping in this selected English river panel. We used the same 3,715 autumn surveys at 217 sites in 1991-2017 for all tests. Early records trained each spatial temperature axis. Other sites tested that axis. Later records tested local change, with site, month, year and pollution controls.

| Recorded unit | Number of labels | Held-out spatial slope | Annual temporal / spatial slope | With identification controls |
|---|---:|---:|---:|---:|
| Family | 79 | 0.925 | 6.3% | 6.4% |
| Fine label, baseline prevalence at least 10 sites | 246 | 0.899 | 1.3% | 5.5% |
| Fine label, at least 30 sites | 151 | 0.907 | 2.1% | 6.4% |
| Fine label, at least 50 sites | 99 | 0.906 | 2.7% | 7.3% |
| Fine label, equal weight to each family | 151 | 0.905 | 2.2% | 6.3% |
| Same 151 fine labels collapsed to parent family | 77 | 0.917 | 5.7% | 5.8% |

The primary fine-label test uses the 30-site threshold, as in the prior family analysis. The other thresholds test sensitivity. Fine labels are the archive's species-group names within each parent family. They include species, genera and coarser groups. This is not a uniform species-level survey.

![Temperature transfer across recorded taxon units](files/transfer.png)

The lines show central 95% ranges from 399 paired site-and-year resamples. They are sensitivity intervals, not a proved confidence procedure. The dashed line is full spatial transfer. The endpoint test compares site means in 1991-2000 and 2008-2017. Identification controls apply only to the annual test.

For 151 fine labels, the annual ratio was 2.1% with a resampling range of -11.7% to 16.0%. With identification controls it was 6.4% (-2.5% to 17.5%). The family range was -1.6% to 15.5%. Thus finer recording did not close this statistical gap. The intervals do not establish that either resolution has a positive annual response.

Endpoint fine-label ratios were larger: 11.7-13.4%, versus 4.2% for families and 5.2% for matched parent families. But the primary fine-label range was -25.0% to 35.8%. These data do not establish strong long-term transfer. With identification controls, the paired fine-minus-parent annual difference was +0.56 percentage points, with a range of -7.75 to +9.31 points. The uncontrolled difference was -3.61 points (-17.53 to +7.77). The endpoint difference was +6.69 points (-22.90 to +31.14). All contrasts are in files/summary.csv. Negative values in the annual contrasts do not prove that family grouping improves measurement of ecological climate response.

The share of distinct label-method records whose names passed a simple binomial text rule rose from 32.7% in 1991-2000 to 45.7% in 2001-2017. This records a change in naming, not verified taxonomic accuracy. Adding that share and the sample's modal abundance method raised the finer-label annual estimate. More detailed records can add observation change as well as ecological detail. Those controls are diagnostic: they may remove real biological change and cannot correct all identification bias.

## Question and prior evidence

Weak transfer of spatial temperature gradients appears in many monitoring systems. SCI 0037934e tested 75 networks. SCI ab21b52e found 4-8% annual thermal transfer in these river records after measured pollution controls. SCI 0bfafb93 extended that test to BOD and found weak transfer there too. Family grouping could miss species replacement inside persistent families. The present study tests that measurement explanation directly on matched surveys and on matched taxon support.

This is a new analysis of raw taxon records, not a fit to the published 54 network summaries. It is not an independent monitoring network or an independent replication of the earlier river panel. The 79-family result exactly reproduces the earlier point estimates and provides an anchor for the resolution comparison.

Prior work already documents thermal change in stream invertebrates. Manfrin et al. (2023; Science of the Total Environment 889, 164278) studied taxonomic and functional change across 3,781 samples. Khaliq et al. (2025; Ecological Indicators 178, 114129) compared six sources of thermal preference in Swiss records. Those studies motivate attention to both resolution and index construction. Our added test holds survey dates, sites, exposure measurements, temporal model and axis-validation design fixed while it changes recorded resolution.

A campaign search also found that a nearby-colonist test had already been done in these rivers (SCI 62c75668). Its uncertain time-direction contrast does not resolve dispersal limitation. We therefore did not repeat it. This resolution audit narrows a different candidate explanation. It does not identify the ecological process that sets the remaining gap.

## Data and selection

Source: Bachiller-Jareno et al. (2025), ChemPop version 2.0, DOI 10.5285/23f194b0-1e21-4f14-be9c-6eabdcc1feb7. Contains data supplied by UK Centre for Ecology & Hydrology. The source combines Environment Agency observations and CHESS-met air temperature. See files/EXTERNAL_DATA.md for attribution, licence, exact shared path, URL and archive hash. files/provenance.json gives all used CSV hashes. No new download was needed.

Selection follows the prior river builder. Keep September-November samples in 1991-2017 and choose one per site-year nearest 15 October, with sample ID as tie rule. Positive abundance defines presence. Repeated family entries are combined by union. Require complete six-month pre-sample temperature, BOD and ammoniacal nitrogen; at least three samples in 1991-2000 and eight in 2001-2017. This leaves 217 of the source's 1,519 sites and 3,715 samples. A zero is lack of recorded detection, not proven absence.

For the family vector retain labels seen at 30 or more baseline sites (79). For finer vectors pair BIO_FAM_NAME with BIO_SPGRP_NAME, remove missing names, and combine duplicates by union. Retain labels seen at 10, 30 or 50 baseline sites (246, 151 or 99). Names and synonyms are not harmonised. Generic and specific records can overlap. No abundance is summed across mixed scales.

The matched family vector takes the union of the same 151 fine labels within each parent family (77 groups), then applies the same presence transformation. It prevents an apparent resolution effect from being caused solely by label support. It is distinct from the original 79-family vector. The family-balanced fine vector first assigns equal total squared weight to each represented family, then divides that weight among its detected fine labels. This checks dominance by families with many labels. All vectors have unit squared norm unless empty. The code defines an empty fine vector as zero; none of these selected surveys had an empty vector (files/vector_checks.json).

## Model

For each vector, use Hellinger coordinates Y_j = sqrt(presence_j / number of detected labels). Average baseline vectors at each site. Regress these means on an intercept, baseline air temperature, mean log(1+BOD) and mean log(1+ammoniacal nitrogen). Baseline temperature is the site term from air temperature regressed on site and year-month effects.

Split sites into two folds within region, with fixed seed 810. Each sample uses a temperature direction g trained in the other fold. Its score is Y dot g / (g dot g). The training slope is one by construction. Held-out baseline regression on the same exposures and fold gives the tested spatial slope. An additional check includes region effects in axis training and validation.

Regress later scores on temperature, log BOD, log ammonia and survey day, with site, month and year effects. The annual ratio is the temporal temperature slope divided by the held-out spatial temperature slope. Survey day is measured relative to mid-October. It adjusts timing but does not model phenology. The identification check adds the binomial-name share and modal abundance-method effects. Other coefficients are not interpreted as ecological causal effects.

Endpoint regressions use changes between the baseline and 2008-2017 site means, with the same four environmental and date changes plus region effects. They do not include the identification controls. Late endpoint coverage can be as low as one sample. The main complete-case panel and windows were inherited from prior work rather than chosen from these fine-label results.

## Uncertainty and validation

Use 399 resamples, seed 271811. Resample sites within region and independently resample years within the baseline and later periods. Use the same draw for every resolution and both annual models. Rebuild baseline community and chemical means, refit directions, and re-estimate spatial and temporal slopes. Hold baseline temperature coordinates, vocabulary and fold assignment fixed. files/bootstrap.csv preserves all aggregate draws. summary.csv includes paired contrasts against the original family vector and the strict matched-family vector.

These are crossed site-and-year sensitivity ranges. They do not cover serial year dependence, river-basin correlation, errors in baseline climate, taxonomic changes or complete-case selection. Spatial slopes shift downward under resampling. For example, the fine-label spatial range is 0.585-0.856, below its point estimate of 0.907. Re-estimating a noisy multivariate direction changes its held-out performance. Precise interval coverage is not established. A ratio range is useful only with a stable positive spatial denominator; summary.csv reports the number of non-positive draws.

The estimator check compares alternating weighted fixed-effect removal with explicit dummy regression on a synthetic unbalanced panel. Maximum projection error is below 2e-12. A separate construction keeps two parent families always present but changes two fine labels within each. The fine thermal score has slope one while family presence has zero variance. Thus the score construction can register within-family change in a controlled example. This is an algorithm check, not ecological validation.

## Meaning and limits

The evidence weakens a narrow explanation: that collapsing the finer labels already available in this archive is sufficient to explain weak annual transfer. It does not rule out hidden species-level change. All resolutions use one archive with mixed identification depth. Unrecorded species, changing taxonomy and undetected populations remain outside the test. No uniform species survey or external species thermal niche was used.

The spatial gradient may contain habitat, river size, geography and water-quality history. It is a descriptive benchmark, not a proven causal equilibrium. Air temperature is a proxy for water temperature. Fixed effects remove shared national change, so these ratios measure conditional local exposure slopes. They are not the fraction of national warming followed. Mean endpoint air-temperature change in the inherited cohort was about -0.03 C, as noted in the prior study. These records cannot establish response to sustained national warming.

The result does not show that pollution control has little value, that ecological response is absent, or that finer identification is unnecessary. It leaves demographic inertia, dispersal, habitat constraints, proxy error and nonlinear response unresolved. The observed naming change also makes a uniformly resolved repeat survey a better test than treating archive fine labels as stable species.

The initial design used family and finer labels, baseline thresholds and identification controls. Matched parent collapse was added after the first point estimates to check taxon support. All reported checks are exploratory. No significance-based threshold selection was used.

## Reproduce

Use Python 3.12 with package versions in files/environment.json. Output must be in separate scratch outside the publication.

From the unpacked publication root:

    export SCI_REBUILD=/absolute/path/to/external_scratch
    sh files/reproduce.sh

This retrieves external data, verifies all used CSV hashes, builds both panels, runs 399 paired resamples, makes summary.csv and transfer.png, and checks the estimator. To reuse the existing shared archive, skip retrieve.py and pass its documented path to build_family.py and build_fine.py. Both use the same --out or --panel scratch directory. analyze.py takes --panel and a separate --out; report.py takes --analysis and --out. Compare the resulting points.csv, bootstrap.csv, diagnostics.json, summary.csv and transfer.png to the bundled files.

Only original text, figures, code and aggregate statistical output are included. No raw or record-level derived external database is bundled. Retrieval and transformation methods preserve reproducibility without changing source rights.

## Research record

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-661700b55db4. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. One finite worker performed this investigation without subagents. Numerical libraries used one thread; no more than two compute processes ran at once. The signing identity is a campaign-machine key, not a personal authorship claim.
