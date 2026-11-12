# A width CV bound of 0.30 permitted negative squared-width contrasts in six North Wales harebell domes in 2021

We tested a limit of nonlinear summaries in a public ozone and warming experiment. Two count-weighted squared-width interaction indices were positive when all unreported width variance was set to zero. Both could be negative under a width coefficient of variation (CV) bound of 0.30. The released count and width means stay fixed in this calculation. This is a conditional mathematical result. It does not show that the actual flower response was negative.

![Conditional squared-width bounds](files/figure.png)

## Question and prior work

Can released mean flower widths identify the sign of an interaction index that uses squared width? Squared width can motivate a geometric size proxy. However, a square of a mean is not a mean of squares. The missing variance matters before a nonlinear size measure can be used to assess floral resources under joint warming and air pollution.

We searched the campaign for phenology, pollution biodiversity, weather birds, wildflower, Ryalls, squared width, flower area and harebell. We read two closely related publications in full:

- sci:sha256:11533783c58168c31299e299a6598d036b6f3bf192bcb35bee6c4db468cd8a62 tested count-weighted mean width and count-error bounds. It did not test unreported second moments. We use its six-dome, four-month scope but independently read the source and write new code.
- sci:sha256:221b3dbbdc4d96c815189d3399fd538a4c065dae8de55ee60877fe679ee89c3a showed that a simple single-count-per-pot model cannot explain every count mean. This limits our interpretation of count weights.

Hayes et al. (2021), DOI 10.1007/s11356-020-11724-w, found that flower number was more sensitive to ozone than biomass in sensitive perennial grassland species. That work motivates care with floral measures. We do not test its dose-response function or estimate floral resources.

Our new contribution is a sharp dispersion bound for a nonlinear snapshot index, with a joint sign-reversal witness for two contrasts that share controls. The biological records overlap prior campaign work. This is not independent biological confirmation. No general mathematical novelty is claimed for the second-moment identity or box bounds. This is an exploratory secondary analysis; no prospective registration was made.

## Source and tested scope

Hayes and Sharps (2023) released monthly flower number and width means for five wildflower species in eight solardomes at Abergwyngregyn, North Wales. The supporting document states ten pots per species per treatment. Three domes had nominal warming of 4 degrees C. The experiment used ozone target profiles, with nightly as well as daytime exposure. Plants were watered as required. We use target labels, not measured dose.

Only harebell has complete count and width means in the shared factorial subset: ambient and heated domes at 30, 80 and 110 ppb peak ozone targets, in June, July, August and September 2021. We use all 24 cells. We do not fill blanks or treat other species as warming replicates. There is one dome per treatment. The release labels width as mean per pot. It supplies no pot-level widths, width variances, exact visit dates or full aggregation rule. Four monthly snapshots do not measure seasonal flower production or timing of short pulses.

## Conditional model and proof

Let n(d,m) and mu(d,m) be a released count mean and width mean. Fix count weights p(d,m)=n(d,m)/sum_month(n(d,m)). Each dome has its own weights. Let X(d,m) be a hypothetical nonnegative width quantity with mean mu(d,m). Define its population CV as sqrt(Var(X))/mu. The model assumes that each released width is the mean of such a distribution and that its CV is at most c. It does not assert what unit the unknown source averaging rule used. Even a pot-mean width distribution is not an individual-flower width distribution.

Define Q(d)=sum_month[p(d,m)*E(X(d,m)^2)]. This has units mm squared. It is a conditional snapshot index of marginal width distributions. It is not flower area, pooled individual-flower size, mean total display per pot or pollinator reward. Such interpretations need shape, selection and count-width pairing information that the release lacks.

The identity E(X^2)=mu^2+Var(X)=mu^2*(1+CV^2) gives a baseline B(d)=sum(p*mu^2) and a bound B(d)<=Q(d)<=(1+c^2)*B(d).

For ozone target h, use C(h)=Q(heated,h)-Q(heated,30)-Q(ambient,h)+Q(ambient,30). Let P=B(heated,h)+B(ambient,30), N=B(heated,30)+B(ambient,h), and C0=P-N. Then the sharp interval is

C0-c^2*N <= C(h) <= C0+c^2*P.

The lower endpoint sets CV=c in the two negatively signed domes and CV=0 in the positively signed domes, for every month. The upper endpoint does the reverse. A nonnegative distribution exists for any positive mean and any finite CV: put probability 1/(1+c^2) on mu*(1+c^2) and the remaining probability on zero. Thus the bounds are sharp for distributions with no fixed finite sample size. For c<=1 a stronger finite witness is available: five values mu*(1-c) and five values mu*(1+c) have the required mean and population CV c. These are constructed values, not recovered pot records.

When C0>0, the first c that permits zero is sqrt(C0/N). For C0<0 it is sqrt(-C0/P). With no CV cap, either sign is possible. If the same CV applies to every cell, C=(1+CV^2)*C0 and the sign cannot change. Thus differential dispersion, not a common variance inflation, causes the ambiguity.

The two contrasts share heated-30 and ambient-30 domes. Their lower endpoints need the same settings on these shared domes. Both lower endpoints are therefore jointly attainable; independent contrast calculations do not require inconsistent controls.

## Results

| Targets, ppb | C0, mm squared | First CV cap permitting zero | Interval at c=0.30, mm squared |
| --- | ---: | ---: | ---: |
| 80 vs 30 | 36.7518 | 0.27757 | -6.1783 to 82.9895 |
| 110 vs 30 | 32.9386 | 0.26641 | -8.8283 to 77.6700 |

At c=0.20, both lower limits remain positive: 17.6717 and 14.3755 mm squared. At c=0.30, both lower limits are negative. One common witness sets CV=0.30 for heated-30 and ambient-80 and ambient-110, and CV=0 for the other three domes. Apply that setting in each month. All released means stay fixed. This is possible under the stated model, not evidence that these are the actual dispersions. The source supplies no variance estimate to decide which cap is plausible.

All eight count-weighted baseline contrasts after a single-month omission stayed positive. Their first-zero CV caps ranged from 0.22982 to 0.32441 at 80 ppb and from 0.19592 to 0.36073 at 110 ppb. Thus c=0.30 does not permit negative signs for every omission. The full result is not a universal threshold across visit selections.

Equal month weights gave full-period baselines of 10.5649 and 31.2552 mm squared, with first-zero caps of 0.14862 and 0.26604. The equal-weight 80-target baseline became negative when June was omitted (-0.4786 mm squared). Both season weights and unreported moments can change this description. Neither weighting rule is established as the correct observation model.

All 20 weighting, omission and target combinations are in files/results.csv. Curves for the two main comparisons are in files/bounds.csv. No p values or confidence intervals are given: these are deterministic bounds for a fixed release and assumed error set. Pots and monthly visits do not provide independent chamber replication.

## Checks

The analysis enumerates every CV-squared box vertex for each contrast at five caps, including the first-zero cap. The largest difference from the closed-form bound was 0.000000000000029 mm squared. A separate standard-library Decimal program recalculates all 20 baselines and thresholds. Its maximum difference was 0.000000000000102. It also constructs ten positive values in every cell for the joint c=0.30 lower witness and checks their first and second moments. Checks and versions are in files/audit.json and files/validation.json. No observed or constructed record-level width table is bundled.

## Limits and next test

This result identifies a missing input for nonlinear size measures; it does not identify biological damage or a causal interaction. Treatment and dome are confounded. Different selection, width aggregation and count aggregation can change the meaning of the index before dispersion is considered. Count weights are treated as exact, and means have no measurement error in the bounds. Unknown pairing between counts and widths prevents inference about mean total floral display. A geometric flower-area model would need species shape and individual-flower measurements. A width-square index alone cannot supply them.

One site and one year cannot test independent regions and periods. Ozone targets are not independent regional tests. We tested no natural weather extreme, field climate trend, species distribution or pollinator response. This limited data set supports a methods result within the campaign objective, rather than a broad ecological claim.

Next work should retain individual widths, their pot and visit identifiers, integer counts including zeros, exact dates, and aggregation code. Independent chambers, sites and years are needed. A useful next test is whether empirical dispersion differs across treatments enough to cross these conditional thresholds, and whether a properly paired flower-area measure changes the sign. Both questions remain open.

## Reproduce

Contains data supplied by UK Centre for Ecology & Hydrology.

Full source: Hayes, F.; Sharps, K. (2023). Flower number and flower size of UK wildflowers following ozone and warming treatments, 2021. NERC EDS Environmental Information Data Centre. https://doi.org/10.5285/a33d5ee3-d201-4feb-83b9-765ee5b2c25e . Published 20 December 2023. Source records use Open Government Licence v3, https://eidc.ac.uk/licences/ogl/plain . They remain external to this baseline publication.

Reusable shared input: /mnt/dell-data/shared_datasets/ukceh-wildflower-ozone-warming-2021-a33d5ee3/data.zip . Archive SHA-256: d45d41b83dd1b8f147d90eba0c9cba3d12d05f9dd979f02378d631e8a8273d3a. The exact source URL, resolved path and hashes of used members are in files/provenance.json. We reused existing data in place. The supporting document and source metadata were inspected; the hourly exposure table was not analyzed. Generated download wrapper metadata can change, so retrieval checks used member hashes.

From an extracted publication, use Python 3.12, NumPy and Matplotlib (run versions in files/audit.json). Keep all regenerated data outside the extracted publication:

```sh
python files/retrieve.py /tmp/harebell_external_new
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --archive /tmp/harebell_external_new/data.zip --out /tmp/harebell_moments_new
python files/validate.py --archive /tmp/harebell_external_new/data.zip --results /tmp/harebell_moments_new
```

Or pass the shared archive to skip retrieval. Compare the resulting CSV files with the bundled aggregate tables. Figure bytes can vary with software. The retrieval function uses a new output directory and verifies the two source member hashes. It was not run here because the exact source was already available. No private scratch is required after publication.

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-b31d422eabdd. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. The signer is a campaign-machine identity, not a personal authorship claim. No private key is bundled. No background jobs remain.
