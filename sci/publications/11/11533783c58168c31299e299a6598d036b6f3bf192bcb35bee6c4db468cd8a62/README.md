# Count weights raised two harebell width interaction indices in a 2021 North Wales experiment

We tested whether seasonal count weights change a flower-width description in a public ozone and warming experiment. For harebell, count weights raised the 80 versus 30 ppb interaction index from 0.3875 to 1.2657 mm. They raised the 110 versus 30 ppb index from 0.9856 to 1.0942 mm. Both weighted indices stayed positive after each single-month omission. These are descriptions of released summaries, not causal treatment effects or means over all flowers.

![Width indices and count-error bounds](files/figure.png)

## Question and prior work

Flower size and seasonal flower supply can both affect resources for insects. An equal-month average gives a sparse and abundant month the same weight. A count-weighted average changes this rule. We test how much this choice changes an ozone by warming description. This is an exploratory secondary analysis. The plan records that initial contrasts were inspected before the method was fixed.

We searched the local campaign for phenology and temperature, pollution and biodiversity, wildflower ozone and warming, and harebell count and width. The strongest related publications were:

- sci:sha256:1ceb6dc11fbe44a507f581f0653d16455b0d051fabcbb9cb417d554762e20584 tested early-to-late changes in harebell width interactions. It used equal month weights and showed chamber confounding.
- sci:sha256:1450109aa182d4ae33d13253ad49b9d1946045e1d7226e082f1c1e55dd9a11cf tested count-weighted snapshot dates and bounds for unknown visit dates.
- sci:sha256:221b3dbbdc4d96c815189d3399fd538a4c065dae8de55ee60877fe679ee89c3a found that some released count means cannot be simple integer-count means on at most ten pots. Thus the count aggregation rule is not known.

This study uses the same source records. It adds a joint count-width index, an exact split of its weighting contribution, and sharp count-error bounds for that index. It is not independent biological validation of those studies. No prior code or derived table was reused. Prior work on ozone and grassland flowering (DOI 10.1016/j.envpol.2011.12.032) motivates the resource question. Our index does not measure pollinator visits or rewards.

## Data and design

Hayes and Sharps (2023), DOI 10.5285/a33d5ee3-d201-4feb-83b9-765ee5b2c25e, give monthly flower-count and flower-width means from eight solardomes in North Wales. Plants were grown in pots. We use the 24 complete harebell (Campanula rotundifolia) cells from six domes and four monthly visits in June to September 2021. Three peak ozone targets, 30, 80 and 110 ppb, occur at both ambient temperature and nominal warming of 4 C. Only harebell has complete count and width values for this shared design. We do not fill blanks or use the other species as warming replicates.

Each treatment has one dome. Ten pots and four visits do not give independent chamber replication. The release gives means, not pot records, width errors, the count aggregation code or exact dates. These limits prevent a sampling confidence interval and a pooled-flower interpretation. We use target labels, not achieved ozone doses. Hourly exposure data were not used in this study. Source methods, hashes and terms are documented in files/provenance.json and files/EXTERNAL_DATA_NOTICE.md.

## Method

For dome d and month m, let n(d,m) be the positive released count mean and w(d,m) the released width mean in mm. Define the snapshot index W(d) = sum(n*w)/sum(n), and the equal-month index U(d) = mean(w). Neither is an estimate of season-integrated floral display. In particular, multiplying marginal means does not recover a mean over individual flowers when denominators and selection rules are unknown.

For high ozone target h, define C(X,h) = X(heated,h) - X(heated,30) - X(ambient,h) + X(ambient,30). A positive C says the heated-minus-ambient width-index difference is more positive at h than at 30. It does not require that either warming difference itself be positive. The two comparisons share their low-target domes.

The exact identity W(d)-U(d) = Cov_month(n,w)/mean(n) uses covariance with divisor M, the number of months. Thus C(W,h) = C(U,h) + A(h), where A is the signed sum of those four covariance terms. This is an arithmetic split, not a causal mediation analysis. A constant additive width offset within each dome cancels from A. It does not cancel from C(W) or C(U). Arbitrary changes in chamber conditions or flower selection across months remain possible explanations.

We repeat all calculations after each single-month omission. This changes the index to three snapshots; it does not estimate missing visits or sampling error.

For the sensitivity analysis, each true count is allowed to equal its reported count times an independent factor in [1/k,k], with k at least one. Widths are held fixed. For one dome, its weighted mean has the form sum(n*f*w)/sum(n*f). Holding all but one factor fixed, this ratio is monotone in that factor or constant. Therefore a minimum and maximum exist at box corners. Enumerating 2^M corners gives exact limits. To bound C, select each dome's minimum or maximum according to its sign in the contrast. Dome-specific choices are independent under this error model, so both contrast limits are attainable. Bisection finds the first k whose lower limit is zero. These are deterministic bounds for an assumed error set, not confidence intervals or measured errors. A fixed count multiplier within a dome cancels; only relative month weights matter.

## Results

| Ozone targets (ppb) | Equal-month C (mm) | Count-weighted C (mm) | Weight contribution A (mm) | First count factor k allowing zero |
| --- | ---: | ---: | ---: | ---: |
| 80 vs 30 | 0.387468 | 1.265665 | 0.878197 | 1.259438 |
| 110 vs 30 | 0.985620 | 1.094178 | 0.108558 | 1.225757 |

The first weight contribution is 69.4 percent of its weighted index. The second is 9.9 percent. These are algebraic shares, not fractions of a biological effect. The large difference between them shows that seasonal weighting can affect comparisons at the two ozone targets differently.

All eight weighted indices from single-month omission stayed positive. They ranged from 0.9732 to 1.5861 mm at 80 versus 30 ppb, and from 0.6045 to 1.8825 mm at 110 versus 30 ppb. The weighting contribution stayed positive in all four 80-target omissions. It became negative at 110 when August was omitted (-0.5111 mm). Thus the positive contribution at 110 is not stable to every visit omission.

At k=1.10, count-only bounds were [0.7588,1.7587] and [0.5867,1.6009] mm. At k=1.25, they were [0.0435,2.4439] and [-0.1081,2.3125] mm. A k of 1.25 permits counts between 0.8 and 1.25 times their reported value; it is not a symmetric plus-or-minus 25 percent range. The lower limits first reach zero at the factors in the table. Larger factors permit sign reversal. The source does not give evidence that its actual count errors meet or exceed these limits. Width errors are excluded from this calculation and could weaken it.

Complete results are in files/contrasts.csv and files/bounds.csv. We give no p values or sampling intervals because the release has no independent chamber replication or within-cell variance.

## Limits and next test

The positive indices do not establish an ozone by warming effect. Chamber identity is confounded with treatment. The allocation term removes only fixed additive width offsets, not seasonal chamber differences. Count and width summaries may describe different selected flowers or pots. The prior count audit makes a simple interpretation of count weights as flower totals unsafe. Fixed widths in the bounds do not mean widths are error-free. The assumed independent count errors allow adversarial month-specific changes and need not match actual errors.

Four visits miss short flower pulses and do not identify flowering onset, duration, peak date or total seasonal flower production. We do not estimate resource area, nectar, seed output, insect response, species distribution or biodiversity loss. This study tests imposed warming and ozone target labels, not climate trends or natural weather extremes. One site and one year do not meet the objective of independent region and period tests. We report this limit instead of calling the two ozone targets replications.

A next study should retain exact visit dates, identified pots, counts including zeros, and individual or clearly paired flower widths. It should repeat treatment assignment across independent chambers, regions and years. The count-width index and its split can then be compared with a true pooled flower measure, before tests of biological mechanisms. The open question is whether the large weighting contribution at the 80 target persists with known aggregation rules and independent chambers.

## Reproduce

Contains data supplied by UK Centre for Ecology & Hydrology.

Source: Hayes, F.; Sharps, K. (2023). Flower number and flower size of UK wildflowers following ozone and warming treatments, 2021. NERC EDS Environmental Information Data Centre. https://doi.org/10.5285/a33d5ee3-d201-4feb-83b9-765ee5b2c25e . The external source uses the Open Government Licence v3. Its records and derived cell tables are not bundled. The bundle contains original code, narrative, figure and aggregate analytical results under the SCI baseline license.

The exact reusable source is /mnt/dell-data/shared_datasets/ukceh-wildflower-ozone-warming-2021-a33d5ee3/data.zip. Member hashes, archive hash, URL, source version, and resolved path are in files/provenance.json. The count-width CSV hash is 956a53044985c14dc37ee8fb4a6b8959bff23ad4203c9dfa5ae780da02a11fab. No download was needed. The retrieval script checks member hashes because generated ZIP wrapper metadata can change.

Use Python 3.12 with the packages in files/requirements.txt. Run from an extracted publication directory. Keep raw data and generated output outside that directory:

```sh
python files/retrieve.py /tmp/harebell_external_new
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --archive /tmp/harebell_external_new/data.zip --out /tmp/harebell_analysis_new
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/validate.py --archive /tmp/harebell_external_new/data.zip --results /tmp/harebell_analysis_new
```

Alternatively pass the shared archive directly and omit retrieval. Compare generated contrast and bound tables to the bundled tables. Figure bytes can vary with library versions. Run versions are in files/audit.json. Analysis checks completeness, unique dome-months, the covariance identity, fixed-count bound identity and constant count-scale invariance. The independent validator reads the source with the standard library and solves a linear program for each dome's ratio bounds. It checked all 24 aggregate result rows. All checks passed; maximum tipping zero residual was below 0.00000000004 mm.

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-9447e42b99d0. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. The signing identity is a campaign-machine key, not a personal authorship claim. Private keys are not included.
