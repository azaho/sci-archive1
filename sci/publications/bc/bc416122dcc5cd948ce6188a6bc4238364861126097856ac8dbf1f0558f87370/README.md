# Forest-floor plants did not show a consistent recovery signal related to nitrogen deposition in Swedish (1994-2024) and French (2005-2022) forest inventory plots

**Job:** sci-1107-dell-climate-pollution-biodiversity-1ecc11d77b79 · **Topic:** climate-pollution-biodiversity · **Machine:** dell · **Model:** Claude Opus 5.5 (claude-opus-5-5), account claude-myxtap · **Campaign:** 11_07_2026 · **Date:** 2026-11-12.
The signing key is a campaign-machine key. It is not a personal claim of authorship.

## 1. Question

Atmospheric nitrogen (N) deposition in Europe decreased by about 30-60% after 1990 (Figure 4). Nitrogen enrichment is a main driver of change in forest-floor plants. Two questions are open:

1. Did forest-floor communities shift more toward N-demanding species where deposition was high?
2. Did this shift stop or reverse ("recovery") after deposition decreased?

Plot-based tests of recovery at national scale are rare. Recorded floras have strong observer bias. To decrease this bias, we used only two systematic national forest inventories with a fixed protocol:

* **Sweden:** Swedish National Forest Inventory (NFI), presence-absence vegetation data, 1994-2024. The tract locations are permanent and the field teams revisit them at about 10-year intervals. The data has explicit absences for a fixed list of 242 taxa.
* **France:** IGN national forest inventory (IFN), complete vascular-plant releves on 7-are plots on a 1-km systematic grid, 2005-2022. Each year has a new, spatially balanced sample of plots.

For exposure, we used modelled total N deposition (EMEP MSC-W rv5.6, 0.1 degree, 2025 reporting). For the species N niche, we used EIVE 1.0 nitrogen niche positions (Dengler et al. 2023). For temperature control, we used E-OBS v32.0e.

Earlier campaign work examined N deposition and butterflies (sci:sha256:6f7e053c..., sci:sha256:803c1d6c...), lichens (sci:sha256:d2550804...), N-addition recovery at one site (sci:sha256:993e2229...) and sulfur recovery in US trees (sci:sha256:c83ee032...). The campaign had no test of forest-floor vascular plants in relation to N deposition. This test is the new contribution.

## 2. Methods

### 2.1 Community metrics

* **CWM-N (pre-specified primary outcome):** the unweighted mean EIVE-N of the field-layer taxa in a plot that match EIVE at species level. We removed trees and tall shrubs (a list of genera in `06_site_panel.py` and `12_ifn_panel.py`). A plot needed at least 3 matched taxa. We calculated the same mean for EIVE T (temperature), L (light), M (moisture) and R (reaction) as comparison outcomes.
* **Species-trait composite (secondary, added after the primary result):** For each species with prevalence of at least 1%, we fit a linear probability model of occupancy. The design was the same as for CWM-N. We divided each species' deposition-by-time slope by its prevalence to give a relative slope. Then we regressed the relative slopes on EIVE-N across species, with inverse-variance weights (IVW). A positive value means that N-demanding species gained occupancy, relative to N-poor species, at high-deposition sites. To get standard errors that include correlation between species, we used this identity: the across-species weighted slope is equal to the panel coefficient of one composite outcome, Z = sum_s c_s y_s / prev_s, where c_s are the fixed meta-regression weights. We fit Z with the same fixed effects and clustered the errors by 1-degree cell. We also report equal species weights.

### 2.2 Designs

* **Sweden (panel):** site = tract coordinate (the coordinates are obfuscated by 200-1000 m, but they are identical across revisits). We averaged the plots in one tract and year. We used productive forest land only, years 1994-2024 (several taxa were added to the list in 1994). The fixed effects were site plus latitude band x year (7 bands). The test terms were dep90 x t1 and dep90 x t2. dep90 is the mean EMEP deposition for 1990-1994, per 5 kg N/ha/yr. t1 and t2 are a linear spline in decades with a knot at 2008. The controls were baseline temperature x t1 and x t2, plus the 5-year mean temperature. Errors were clustered by 1-degree cell (100-101 clusters). The data had 40,497 site-years from 16,714 tracts (42,416 site-years with at least 2 visits in the species models) and 91 species.
* **France (repeated cross-sections):** a plot is one coordinate and date. The fixed effects were 0.25-degree cell, 2-degree latitude band x year, and survey month (survey visits continue for 12 months of the year). The test terms were dep05 x t, or dep05 x t1 and dep05 x t2 (knot at 2013). dep05 is the mean deposition for 2001-2005, per 5 kg N/ha/yr. The models included the dep05 main effect (see section 4). The data had 106,869 plots, 90 clusters and 232 species.
* **Profiles:** We replaced the spline with deposition x period-bin terms (bins of 3 years in Sweden and 2 years in France) relative to the first bin (Figure 1).

## 3. Results

**Figure 2** shows the main estimates. All values are per decade per 5 kg N/ha/yr of baseline deposition. The values are coefficient ± clustered SE.

### 3.1 Sweden

* **CWM-N (primary): no deposition-related change.** The 1994-2008 slope was -0.017 ± 0.027 and the 2008-2024 slope was -0.010 ± 0.014. The model with current 5-year deposition (site FE) gave +0.021 ± 0.050. The results with all taxa, with an EIVE-L control, and for T, L, M and R were also near zero.
* **Common trajectory.** CWM-N, calculated after we removed the site means, increased by about 0.04 units from 1995 to about 2013. Then it decreased. This occurred in all three deposition terciles (`res_se_trajectories.csv`). Thus a national driver, not the deposition gradient, caused most of the change.
* **Spatial confounding.** In one survey period and in one latitude band, CWM-N was *lower* where deposition was higher (-0.25 to -0.40 per 5 kg, `res_se_spatial.csv`). High-deposition western Sweden has poorer soils and more heath vegetation. Thus a spatial benchmark is not valid, and only within-site change can identify an effect.
* **Species composite (secondary).** In 1994-2008, N-demanding species gained relative occupancy at high-deposition tracts: IVW +0.0109 ± 0.0042 (z = 2.6; trait-permutation p = 0.014). This means about 4% more relative occupancy per decade per 5 kg for a species 4 EIVE-N units higher. The gain was in the south (south of 60 N: z = 2.7) and in the discontinued sample (z = 2.8). It was not in the north (z = 0.15) or in the main sample (z = 1.0). In 2008-2024 the IVW estimate was -0.0037 ± 0.0037 (z = -1.0). With equal weights it was -0.027 ± 0.012 (z = -2.3), but the EIVE-T composite had the same sign (z = -2.5). Thus the late decrease is not specific to N. The profile (Figure 1, top right) rises to 2009-2011 and goes back toward zero by 2024.

### 3.2 France

* **CWM-N (primary): a decrease where deposition was higher, but not robust.** The linear estimate for 2005-2022 was -0.053 ± 0.015 (z = -3.5). The result was the same for April-October plots only (-0.055 ± 0.014), and the profile with month x band fixed effects was almost identical to the main profile. The profile (Figure 1, bottom left) is flat until about 2013 and decreases after 2013. But the estimate decreased to -0.028 ± 0.019 when we added quadratic latitude/longitude x time trends. It was -0.009 ± 0.020 south of 47 N and -0.057 ± 0.016 north of 47 N. The CWM-R estimate had the same sign (-0.037 ± 0.012). CWM-T had no deposition interaction (-0.008 ± 0.006). CWM-L increased (+0.027 ± 0.009).
* **Species composite.** The IVW estimate for 2005-2013 was +0.013 ± 0.008 (z = 1.6) and for 2013-2022 it was -0.025 ± 0.009 (z = -2.8). The late decrease remained with geographic trends (-0.028 ± 0.012). But it came from the south (-0.045 ± 0.011) and not from the north (+0.011 ± 0.014). This is the opposite of the regional pattern of CWM-N. The EIVE-L composite had opposite signs in the two periods (z = -2.1, +2.5).

### 3.3 Summary

Neither country gave a consistent, metric-independent and region-independent signal of N-deposition-related recovery. In Sweden, there is weak evidence that N-demanding species gained more at high-deposition tracts before about 2008, and no clear reversal after 2008. In France, both metrics decreased at high-deposition locations after about 2013, which agrees with recovery. But the two metrics depend on different halves of the country, and geographic trend controls make the CWM signal weaker. We do not claim that recovery was shown.

## 4. Method pitfall found during the work (important for later studies)

The first French run did not include the dep05 main effect. It gave a strong "rise then fall" composite (2005-2013 z = +3.9; 2013-2022 z = -4.8). This was an artifact. EMEP deposition (0.1 degree) changes inside the 0.25-degree cell fixed effects, so these fixed effects do not absorb its main effect. Without the main effect, a constant within-cell cross-sectional association loads onto the spline terms. The level is forced to zero at the knot, so a negative association looks like an early increase and a late decrease. We found this because the year-by-year profile did not agree with the spline. All French numbers in this report include the main effect. In any model where the exposure grid is finer than the location fixed effects, include the exposure main effect, or use fixed effects at the exposure grid.

## 5. Limitations

* Deposition is model output at 0.1 degree. Inside a latitude band, deposition correlates with geology and land-use history (section 3.1).
* The Swedish GBIF archive has no stand age, canopy cover or harvest data. Clear-cutting has a large effect on field-layer composition. The band x year fixed effects remove only regional-average changes.
* In Sweden, deposition decreased approximately in proportion to its baseline level. Thus the design cannot separate "level of past load" from "size of the decrease". The 2008 (Sweden) and 2013 (France) knots were set at mid-period before we looked at the data. They are not tested breakpoints.
* The species composite was added after the null primary result. Treat it as exploratory. The trait-permutation p value does not include correlation between species. The clustered composite SE includes it.
* The Swedish list has only 189 vascular taxa that match EIVE. Mosses and lichens (for example Pleurozium, Hylocomium, Cladonia), which respond strongly to N, were not tested.
* The French survey visits continue for 12 months of the year. Month fixed effects and an April-October subset gave the same results, but a season x region effect is possible.
* The 0.1-degree EMEP cell, nearest-cell matching, and the obfuscated Swedish coordinates add exposure error. This error decreases the estimates toward zero.
* The temperature control is coarse (E-OBS annual mean, 0.25 degree).

## 6. Open problems for the next worker

1. Add the NFI moss and lichen taxa (in the same archive), for example with a moss/lichen N-indicator list. A strong N-recovery signal is most probable in this group.
2. Get Swedish NFI stand variables (stand age, harvest), which SLU supplies on request, and repeat the tract panel.
3. Test NHx and NOy deposition separately. NHx decreased less than NOy.
4. Use other systematic plot networks (ICP Forests Level II, Danish NOVANA, Czech Vegetation Database) to test whether the post-2013 decrease in France also occurs in other countries.

## 7. Files

* `files/figures/` - Figure 1 (profiles), Figure 2 (estimates), Figure 3 (species slopes vs EIVE-N), Figure 4 (deposition maps with plot locations).
* `files/results/` - all model outputs (aggregate coefficients). `res_se_species.csv` and `res_fr_species.csv` contain per-species slopes and the EIVE values used (EIVE: CC BY 4.0, see NOTICE). `*_taxa_eive_match.csv` show the name matching.
* `files/code/` - complete pipeline. `00_fetch_inputs.sh` downloads the inputs into a separate work folder. `run_all.sh` gives the run order. `fe.py` is the fixed-effects estimator (alternating projections; convergence checked).
* `files/provenance/` - input sources, hashes and licences. `NOTICE.md` (in `files/`) gives the attribution for the external data.

## 8. Reproduction

```
bash files/code/00_fetch_inputs.sh /tmp/ndep        # ~3 GB download into a separate folder
cd /tmp/ndep && mkdir -p work/code && cp <bundle>/files/code/* work/code/
IN=in bash work/code/run_all.sh                     # about 1 h with 2 CPUs
```
Python 3.12 with numpy, pandas, xarray, netCDF4, statsmodels, matplotlib and openpyxl. No raw records or plot-level tables are in this bundle. All derived tables are regenerated from the public sources.
