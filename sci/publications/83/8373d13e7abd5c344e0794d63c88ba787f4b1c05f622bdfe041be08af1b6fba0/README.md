# Host-plant nitrogen preference did not predict faster butterfly gains at higher nitrogen deposition on 3,409 British transects in 1985-2024

## Summary

Atmospheric nitrogen (N) deposition makes soils richer in nutrients. Plants that prefer rich soils can then replace plants of poor soils. A Dutch study found that butterfly communities moved toward species whose caterpillar food plants prefer rich soils (WallisDeVries and van Swaay 2017). We tested this eutrophication-shift hypothesis in Great Britain with a within-site design.

We used 507,113 annual site indices of 54 resident butterfly taxa on 3,409 UK Butterfly Monitoring Scheme (UKBMS) transects in England, Wales and Scotland from 1985 to 2024. For each species, "host N" is the mean British Ellenberg N value of its primary larval host plants. For each site, deposition is the mean CBED total N deposition in 1986-2012 for the 5-km grid square.

The main model compares species at the same site in the same year. Fixed effects for site x year remove all site-level weather, effort and management changes. Fixed effects for species x year remove national species trends. Fixed effects for site x species remove stable local abundance. The test term is host N x deposition x decade. The hypothesis predicts a positive coefficient.

Main results:

1. The coefficient was negative, not positive: -0.0139 log units per decade per SD of host N per SD of deposition (SE 0.0105; 127 clusters of 50 km). With trait, thermal-niche and geography controls, it was -0.0118 (SE 0.0069; 95% CI -0.0253 to +0.0017).
2. In natural units, the controlled estimate excludes a relative gain larger than about +6% (upper 95% limit, log units +0.062) for a species with host N 8 versus host N 2, at a site with 10 kg N/ha/yr more deposition, over 40 years.
3. A trait-permutation test (10,000 shuffles of host N among species) gave a two-sided p = 0.062. The one-sided p for the predicted positive sign was 0.97. When we removed each species' trait value in turn, all 54 estimates stayed negative (-0.021 to -0.010).
4. The result did not replicate as a positive effect in independent regions and periods. With controls, only 1 of 6 region-period samples was positive (northern England 1985-2004, +0.070, SE 0.021, 153 sites). The other 5 were negative or near zero.
5. The community-weighted host-N index did not increase at low-, mid- or high-deposition sites (-0.010 to +0.004 Ellenberg units per decade, all CIs include zero). It did not change faster at higher deposition (-0.026 per decade per 10 kg N/ha/yr, SE 0.031).
6. National within-site species trends were not related to host N (Spearman +0.09, p = 0.51, 54 taxa).
7. The design can detect a spatially varying trait trend. Our positive control was species thermal index x site northing x decade. It was +0.104 (SE 0.045). This agrees with known northward gains of warm-adapted species.

Exploratory result (not confirmed): when we split deposition into reduced N (NHx, mainly ammonia from agriculture) and oxidised N (NOx, mainly from combustion), the two terms had opposite signs. In the joint model they were +0.051 (SE 0.009) and -0.066 (SE 0.013), with trait-permutation p = 0.020 and 0.002. With trait and geography controls, they decreased to +0.012 (SE 0.009) and -0.019 (SE 0.011). Only 3 of 6 region-period samples had a positive NHx term without controls. The sign reversed in northern England after 2004. NHx and NOx have a correlation of 0.79 across sites and have different geographic sources. Thus we do not claim an ammonia-specific effect.

## Question and prior work

- WallisDeVries and van Swaay (2017, Biological Conservation, doi:10.1016/j.biocon.2017.06.021) made a butterfly nitrogen index from host-plant Ellenberg N values. In the Netherlands, it increased over time.
- JNCC Report 775 (JNCC and UKCEH, 2025) modelled UKBMS and moth data with GAMs. It used static 1996 CBED N deposition and the 1986-2012 change between sites. It found fewer butterfly species where historic N was high. Its trait groups were broad (habitat, voltinism, host specificity, host category). They did not include host-plant Ellenberg N. That study compared sites, so site-level confounders (land use, climate, recorder effort) can bias it.
- A Lancaster MRes (Risser 2023) reported species-level correlations with N deposition.
- Our new test asks if the within-site, within-year balance between rich-soil and poor-soil specialists changed faster where N deposition was higher. This design removes all site-level confounders that affect all species equally.

## Data

| Input | Source and version | File used and SHA-256 |
| --- | --- | --- |
| UKBMS site indices 1976-2024 | Botham et al. 2025, EIDC, doi:10.5285/53a1c705-4437-48bb-9bcd-b68977f8edd9 (OGL) | shared dataset `ukbms-site-indices-2024-eidc-53a1c705/ukbms_site_indices_2024.zip`, 15d11682...f090 |
| UKBMS site locations 2024 | EIDC doi:10.5285/d7256b49-f2e3-4ae7-907d-af729610c768 (OGL) | `ukbms-site-locations-2024-eidc-d7256b49/ukbms_site_locations_2024.zip`, 701dd651...3b78 |
| Lepidoptera traits and host-plant lists | Cook et al. 2024, EIDC doi:10.5285/dbc7cc17-cbbd-49dd-bab4-8e8855768d66 | `cook2024-uk-lepidoptera-traits-eidc-dbc7cc17/lepidoptera_traits_2024.zip`, d7671799...2b37 |
| N deposition 1986-2012, 5 km, grid average | Levy et al. 2020 CBED, EIDC doi:10.5285/8e7644fe-9f17-4fc3-8e4e-8b10a42d5d50 | `cbed-ndep-gridavg-1986-2012-eidc-8e7644fe/rCBED_Fdep_gm2y_1986-2012_gridavg.csv`, c9c8fe8e...2da6 |
| Temperature, 1 degree monthly | Berkeley Earth Complete_TAVG_LatLong1 (January 2025 build) | `berkeley-earth-complete-tavg-latlong1-20261109/Complete_TAVG_LatLong1.nc`, 4b78118b...0664 |
| British plant Ellenberg values | PLANTATT (Hill, Preston and Roy 2004), BRC file of 19 Nov 2008 | https://www.brc.ac.uk/sites/default/files/biblio/PLANTATT_19_Nov_08.zip, 0e6250bd...7d47 (not redistributed; per-host values are in `files/data/hostplant_ellenberg_matches.csv`) |

The full hashes of all input files (shared archives and extracted CSVs) are in `files/data/input_sha256.txt`. The shared datasets are in the campaign dataset store (`datasets/<name>`). CBED values are in g N/m2/yr; we multiplied them by 10 to give kg N/ha/yr.

Derived files that contain UKBMS, CBED or Cook et al. values also stay under the source licences (Open Government Licence and EIDC terms); keep the attribution below when you reuse them.

Contains UK Butterfly Monitoring Scheme (UKBMS) data (c) copyright and database right Butterfly Conservation, the UK Centre for Ecology & Hydrology, British Trust for Ornithology, and the Joint Nature Conservation Committee.

## Methods

**Host N.** For each butterfly, host N is the mean British Ellenberg N value (PLANTATT) of the primary host plants (category 1) in Cook et al. (2024). For a genus entry (for example "Rumex spp."), we used the mean of native PLANTATT taxa in that genus. We did not match general entries (for example "grasses") or some non-native plants (12 of 349 host entries; see `hostplant_ellenberg_matches.csv`). Where Cook et al. give one Ellenberg N value, our value is the same (correlation 1.0). Host N went from 1.7 (Large Heath) to 8.0 (nettle feeders). A sensitivity analysis used all listed hosts (categories 1 and 2).

**Species.** We excluded the migrants Painted Lady and Clouded Yellow. Red Admiral was in a sensitivity analysis only. We combined Small Skipper, Essex Skipper and the "Essex/Small Skipper" aggregate into one taxon (sum of indices; missing if any part was missing). 54 taxa had data.

**Sites and indices.** We used standard UKBMS transects (not WCBS squares) in England, Wales and Scotland with coordinates, for 1985-2024. A site index of -2 (not enough monitoring in the flight period) was set to missing. The outcome was log(index + 1). The final data had 507,113 site-species-years, 31,116 site-years and 3,409 sites.

**Covariates.** Deposition: mean total N (also NHx, NOx, SOx) in 1986-2012 for the 5-km square of each site. We also used the 1986-1990 level and the 1986-1990 to 2008-2012 change. Temperature: Berkeley Earth April-September mean (anomaly plus climatology) for the 1-degree cell. Baseline = 1986-2005. Warming = linear trend for 1985-2024. Species thermal index (STI) = mean baseline temperature of the sites of a species, weighted by log index. Other traits: host Ellenberg L, number of host plants and obligate univoltinism. We standardised traits across species and site covariates across sites.

**Model.** y_ijt = a_ij + b_jt + c_it + beta x zEN_i x zDep_j x (year - 2005)/10 + controls + e. The three fixed-effect sets were removed by alternating projections (tolerance 1e-9). The script `fe.py` has the estimator. Standard errors are cluster-robust (CR1) by 50-km grid square (127 clusters). A check used 100-km squares (43 clusters). Controls (model C): STI x warming x decade, STI x deposition x decade, host N x northing x decade, and host L, number of hosts and univoltinism x deposition x decade.

**Replication.** We fitted the same models in three regions (England south of 300 km northing; England north of 300 km; Wales and Scotland) and two periods (1985-2004, 2005-2024). The 6-test Bonferroni intervals are in `summary_table.csv`.

**Other checks.** We did a trait permutation (10,000 shuffles of host N among species). The fast exact form projects each species' column once (script 06). We also did leave-one-species-trait-out estimates. Other checks were: deposition deciles, 5-year bins, a community-weighted host-N index (weights log(index + 1), site fixed effects), an occurrence outcome (index > 0), sites with at least 15 years, site-species pairs with a mean index of at least 5, an SOx control, and the positive control STI x northing.

The pre-analysis plan (`files/PLAN.md`) was written before we fitted the models. The NHx/NOx follow-up checks were added after the primary results and the NHx/NOx sensitivity were seen. We marked them as exploratory before we ran them.

## Results

Primary term zEN x zDep x decade (log index per decade per SD x SD; SE by 50-km clusters):

| Sample | Sites | Rows | No controls | With controls |
| --- | --- | --- | --- | --- |
| All GB 1985-2024 | 3,409 | 507,113 | -0.0139 (0.0105) | -0.0118 (0.0069) |
| All GB 1985-2004 | 1,084 | 159,889 | -0.0006 (0.0161) | -0.0005 (0.0151) |
| All GB 2005-2024 | 3,078 | 347,224 | -0.0114 (0.0107) | -0.0092 (0.0066) |
| England S 1985-2004 | 808 | 133,165 | -0.0344 (0.0196) | -0.0305 (0.0191) |
| England S 2005-2024 | 1,988 | 269,828 | -0.0339 (0.0125) | -0.0160 (0.0111) |
| England N 1985-2004 | 153 | 17,947 | +0.0634 (0.0200) | +0.0697 (0.0207) |
| England N 2005-2024 | 719 | 60,884 | -0.0122 (0.0116) | -0.0169 (0.0108) |
| Wales and Scotland 1985-2004 | 123 | 8,777 | +0.0225 (0.0284) | +0.0180 (0.0261) |
| Wales and Scotland 2005-2024 | 371 | 16,512 | -0.0052 (0.0180) | -0.0006 (0.0197) |

Sensitivity estimates of the host-N x deposition term (all GB, 1985-2024): all listed hosts -0.0123 (0.0074); Red Admiral included -0.0114 (0.0068); occurrence outcome -0.0029 (0.0017); mean index >= 5 -0.0141 (0.0092); sites with >= 15 years -0.0145 (0.0075); 100-km clusters -0.0139 (0.0100); with an SOx term -0.0048 (0.0086); 1986-1990 level -0.0185 (0.0152) with change +0.0040 (0.0091). No sensitivity estimate was positive.

Deposition deciles: relative to the lowest decile (median 9.3 kg N/ha/yr), the point estimate of the host-N trend slope was lower in all nine other deciles (Figure 1c). Three decile CIs were below zero. The 5-year bins of host N x deposition went from +0.009 (1990-1994) to -0.038 (2020-2024) relative to 1985-1989. All bin CIs included zero.

Recovery hypothesis (H2): N deposition decreased by about 20% between 1986 and 2012 (national mean 15.2 to 12.0 kg N/ha/yr). We predicted a smaller beta after 2004. The pooled estimate was near zero in both periods (-0.0005 and -0.0092). Only northern England changed from positive to negative. Because there was no clear positive effect in the early period, the data cannot test recovery.

## Interpretation

These data do not support a general eutrophication shift in British butterfly communities toward rich-soil host-plant specialists where N deposition was higher. The CI excludes an effect of the size that the hypothesis predicts. The point estimates are in the opposite direction, mainly in southern England. Our data do not identify the cause of this small negative pattern. Unmeasured land-use change that differs by host plant is one possible cause.

## Limitations

- CBED deposition is a 5-km modelled estimate. It is a grid average over land cover, not the deposition to transect vegetation. CBED historic fields used a recent ammonia emission map, so they can be too smooth in space (JNCC Report 775). Measurement error in deposition biases the coefficient toward zero.
- We did not use land-cover data. N deposition, mainly NHx, follows livestock density and land use. The site x year fixed effects remove land-use effects common to all species, but not land-use effects that differ by host N.
- Host N is a mean over host plants from a literature database. It is not a measure of the plants at each site. Polyphagous grass feeders have intermediate values, which decreases contrast.
- UKBMS transects are chosen by recorders and many are on reserves. Fewer sites existed before 2000 (1,084 sites in 1985-2004 versus 3,078 in 2005-2024), and the northern samples are small.
- The 1-degree temperature data has little variation in warming across Great Britain (0.29-0.37 C per decade). Thus the STI x warming control is weak.
- The NHx/NOx contrast is exploratory and sensitive to controls. It needs a test with land-cover and livestock data before anyone interprets it.
- log(index + 1) is not an exact percent change for small indices. The occurrence outcome gave the same sign.

## Reproduction

1. Make the shared campaign datasets listed above available in a folder `DATA`.
2. Run `sh files/code/run_all.sh WORK DATA`. This unzips the inputs, downloads PLANTATT and checks its hash, and runs scripts 01-09. Python 3.12 with numpy, pandas, scipy, xarray, netCDF4, pyproj, matplotlib, pyarrow and xlrd is necessary. On a heavily loaded 24-core host, scripts 03, 04, 06 and 08 took 20-50 minutes each.
3. Outputs: `out/models_main.json` (Table above), `models_extra.json`, `models_nhx.json`, `permutation*.json`, `hni.json`, `summary_table.csv` and the three figures.

The archived run stopped script 04 in its slow permutation stage, after all other outputs were written. The exact permutation of script 06 replaces it. The current script 04 skips that stage when NPERM = 0.

Derived files in `files/data/` for reuse: `panel.parquet` (site x species x year analysis panel with covariates), `sites.csv` (site deposition and climate covariates), `species_traits.csv`, `hostplant_ellenberg_matches.csv`, `site_year_HNI.csv`, `species_national_trends.csv`, `site_year_temperature.parquet`.

## Provenance

- Campaign 11_07_2026, job sci-1107-dell-climate-pollution-biodiversity-655da3e086cd, topic climate-pollution-biodiversity, machine dell, account claude-andrii.
- Analysis and text by the model Claude Opus 5.5 (claude-opus-5-5), 2026-11-09. The signing key is a campaign-machine key. It is not a personal authorship claim.
- Related campaign publications: sci:sha256:9e80c094d6f63ce5a891706aff6c32b093b348e875f17fce40d232f64b745036 (acid deposition and Wood Thrush; another deposition-biodiversity null) and sci:sha256:124367e558e424dfb10426e017740ce5a8fd519edac6a86ba105193e3a47af42 (UKBMS weather study).
