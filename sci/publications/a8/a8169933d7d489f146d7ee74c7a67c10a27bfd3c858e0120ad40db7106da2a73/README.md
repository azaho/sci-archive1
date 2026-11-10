# Capped SST exposure keeps a positive 1982-2025 trend under 0.05 C errors and three arbitrary errors per cell-year and baseline pool in a one-degree OISST sample

Annual capped warm exposure has a positive 1982-2025 trend in a fixed NOAA OISST v2.1 sample under a joint small-error and sparse-error class. The result holds with both tested seasonal baselines. The smallest safe lower slope is **+0.554 equivalent days per decade**. The input class allows at most three errors of any finite size per cell-year and at most three corrupt entries in each seasonal baseline pool. Every other daily input can change by at most 0.05 C. The baseline thresholds are calculated again from the changed inputs.

These are conditional sensitivity bounds. We do not show that actual SST errors meet these limits. The result concerns one capped daily response in one revised product and a fixed point sample. It does not identify the physical source of warming or establish a statistical trend confidence level.

![Capped exposure bounds](files/bounds.png)

Figure 1. Safe lower trend bounds for the 1 C cap, 1982-2025. The parameter k limits corrupt dates per cell-year. The parameter r limits corrupt entries per 330-entry seasonal baseline pool. Both restrictions apply to the same set of corrupt dates. Points are the tested cases; lines are guides, not additional certificates. Negative lower bounds are unresolved signs, not demonstrated reversals. The blue curve excludes arbitrary errors. These curves are sensitivity bounds, not confidence intervals.

## Question and prior work

The selected SCI publications show that satellite input changes put steps into fast SST variance and affect marine heatwave counts, duration, intensity and front statistics. Later studies establish conditional trend bounds for heatwave days, connected area and positive threshold-excess dose. Our source files and spatial sample match those studies. This is a new method and sensitivity test, not an independent observational confirmation.

The closest prior work is SCI publication **6b5e961c...**, which tested uncapped all-day and event-restricted positive threshold-excess dose under uniform amplitude limits. A local campaign search found that result after raw extraction had begun. We stopped the duplicate question and recorded a new design before any capped-exposure result. [design.md](files/design.md) preserves that choice. SCI publication **825d6796...** also uses rank bounds for a few arbitrary baseline errors in event-day tests. Its event-day corruption allowance includes propagation through run rules. We use a bounded daily response without an event gate and an exact annual correction over possible corrupt dates.

We ask: can a useful severity indicator keep a trend sign when a limited set of input errors has no amplitude bound? A uniform small-error certificate excludes every larger error. That is a strong restriction in a long daily record. Capping permits an explicit tradeoff: it limits the influence of extreme errors but discards severity differences above the cap.

Hobday et al. (2016), doi:10.1016/j.pocean.2015.12.014, defines standard event metrics. Schlegel et al. (2019), doi:10.3389/fmars.2019.00737, tests data limitations. NOAA's [marine heatwave indicator](https://ecowatch.noaa.gov/thematic/marine-heatwaves) describes cumulative degree-day intensity. Our measure differs from those standard metrics. [literature.md](files/literature.md) gives the targeted search and the scope of the method claim. We do not claim to invent clipping, quantile rank bounds or degree days.

## Data and response

We read and hash-checked 44 annual NOAA PSL OISST files for 1982-2025. All hashes match store provenance and the earlier signed sample study. OISST retains v2 values before 2016. The fixed sample contains **29,120 native pixels** at one-degree spacing between 60 S and 60 N, over **16,071 days**. Every source pixel has a complete record above -1 C. These are sampled native values, not one-degree means. The mask and cosine latitude weights stay fixed in every case. [sources.json](files/sources.json) records exact shared paths, URLs, byte counts and SHA-256 hashes; [source_audit.json](files/source_audit.json) records the sample checks.

At each cell, the seasonal threshold T is a local 90th percentile. It uses 11-day actual-time pools around each non-leap centre date in a 30-year baseline, linear sample percentile interpolation, an interpolated February 29 and a 31-day circular mean. Each pool contains 330 entries from 30 centre years. It is not a contiguous 330-day interval. Pools can extend five days outside the named baseline. We test 1983-2012 and 1991-2020. No warming trend is removed.

For positive cap c, the daily response is:

`f = min(max(SST - T, 0), c) / c`.

Annual capped exposure is the sum of f over calendar days. It has units of **equivalent saturated days**. With the primary 1 C cap, an excess of 0.5 C contributes half a day and an excess of 1 C or more contributes one day. All days contribute; there is no five-day event gate or gap join. This measure is neither degree-day dose above the seasonal mean nor ocean heat content. It is not a measured species response.

The primary case was c=1 C, non-corrupt error limit e=0.05 C, annual corrupt-date limit k=3 and pool limit r=3, with both baselines and the full endpoint. Controls use caps 0.5 and 2 C, e=0, 0.10 and 0.14 C, paired limits r=k=0, 1 and 5, a 2021 endpoint, the tropics, and pooled extratropics. All planned cases are reported.

## Method and new result

[method.md](files/method.md) gives the proof. At each cell, choose one set of corrupt dates. Outside that set, the changed SST differs from the source by at most e. At corrupt dates it can take any finite value. The same set must meet both the annual limit k and the limit r in every baseline pool. Each baseline defines its own family of pools; a joint two-baseline statement requires both families of restrictions.

Replacing at most r pool entries moves each source order statistic by at most r ranks. The new q90 is therefore bounded by the source quantiles at ranks shifted down and up by r, with a further e allowance for the small errors. Interpolation and positive smoothing preserve these bounds. They give daily lower and upper margins at non-corrupt dates, including changes in the baseline.

Apply the capped response to get non-corrupt daily bounds l and u. A corrupt date can contribute any value in [0,1]. A safe annual lower bound is `sum(l) - sum(k largest l)`. A safe upper bound is `sum(u) + sum(k largest (1-u))`. These corrections cover every possible placement of the allowed bad dates. They are sharp for the relaxed independent daily intervals, but need not be jointly sharp with the baseline-pool constraints.

Nonnegative spatial weights preserve annual bounds. OLS trend weights have both signs. The lower slope uses upper annual values at negative weights and lower values at positive weights. The upper slope exchanges them. A trend in a lower annual envelope alone would not be a safe lower trend bound.

A related impossibility result explains the cap. One arbitrarily large positive error on an early date outside all baseline pools leaves T unchanged and makes ordinary all-day degree-day dose arbitrarily large in that early year. Its negative OLS year weight sends the dose slope to negative infinity. A late positive-weight date sends it to positive infinity. Thus uncapped dose has no finite two-sided slope bound in this one-error class. Capping limits the direct annual effect of one date to one equivalent day. Omitting the event gate also avoids propagation through event rules. Baseline errors can still affect many dates, so rank envelopes remain necessary.

## Results

### The planned joint error class retains positive full-record trends

All slopes below are equivalent days per decade, for the 1 C cap and the spatial mean over the full sample.

| Baseline | Source slope | Safe lower slope | Safe upper slope |
| --- | ---: | ---: | ---: |
| 1983-2012 | 9.201 | **2.568** | 16.081 |
| 1991-2020 | 5.772 | **0.554** | 11.284 |

The bounds allow e=0.05 C, k=3 and r=3. Every record in this class has a positive slope. The allowed rate range is broad. The result supports a sign under the stated assumptions, not the raw rate as a precise climate estimate.

![Annual capped exposure](files/annual.png)

Figure 2. Source annual exposure and annual envelopes for the primary class, c=1 C, e=0.05 C, r=k=3. Envelopes need not be attained together by one changed record. Their slopes alone are not the reported safe trend bounds.

### Larger errors, a later baseline and the endpoint limit the guarantee

At e=0.10 C and r=k=3, the lower slopes are -0.774 and -1.812 for the two baselines. Both signs are unresolved. Even with r=k=1, the later-baseline lower slope is -0.195 at this dense-error limit. At e=0.05 C and r=k=5, the earlier-baseline lower slope remains +0.643, but the later-baseline lower slope is -1.062. These are failed certificates, not constructed reversals.

When non-corrupt inputs stay unchanged (e=0), five arbitrary errors per cell-year and per pool still leave positive lower slopes of +4.028 and +1.349. This case allows large sparse errors but no small widespread errors. It must not be confused with the primary joint class.

Through 2021, the primary 1 C lower slopes are +0.282 and -1.435. The two-baseline result therefore depends on the later years. It cannot separate recent physical warmth from observing-system changes.

The cap also matters. In the full record and primary error class, the 0.5 C cap gives positive lower slopes of +4.571 and +1.655. The 2 C cap gives +0.896 and -0.221, so the two-baseline certificate fails there. Caps define different indicators; these rates are not interchangeable estimates of physical heat dose.

![Cap and endpoint checks](files/controls.png)

Figure 3. Primary-class lower slopes under cap and endpoint changes. A higher cap retains more severity information but can weaken this sign certificate. Lines connect tested caps only.

### The spatial mean is not a common regional guarantee

For the primary 1 C cap and full record, the tropical lower slopes are +0.308 with the earlier baseline and -1.122 with the later baseline. The corresponding pooled extratropical slopes are +4.311 and +1.848. The full-domain guarantee does not apply to every latitude band or individual cell. Every regional result is preserved in the tables.

## Validation and evidence

All checks pass. [validation.json](files/validation.json) records 420 independent sparse-sum enumerations, 300 quantile-rank tests, 2,112 accelerator comparisons with direct annual calculations, 216 cases with thresholds rebuilt after synthetic changes, and eight batched-versus-single-rank threshold comparisons.

The real-record check uses three fixed cells. It inserts one value of plus or minus one million C per year for all 44 years, together with a small step of at most 0.05 C elsewhere. The corrupt-date schedule has at most one corrupt entry in any tested baseline pool. Complete threshold rebuilding stays within the primary envelopes for both baselines and all caps. [real_validation.json](files/real_validation.json) preserves counts, actual slopes and bounds. This deliberate stress test is not a claim about real ocean values or a full-domain changed record.

The aggregate audit recalculates all **576 slope rows** from **12,672 annual rows** and checks error-budget nesting, bound ordering and annual ranges. The reported slope round-trip error is zero at the stored precision. [aggregate_audit.json](files/aggregate_audit.json) gives the result. Finite tests support the code; the proof supplies the general bound.

The accelerator sorts annual margins once, uses prefix sums and binary search for capped sums, and reads the required extreme values for the sparse corrections. It is checked against direct clipping and partial sorting. Numerical guards expand nonzero-error margin bounds by 1e-10 C and annual bounds by 1e-9 equivalent day. This is not formal interval arithmetic.

## Limits and use

- No actual error budget is estimated. An RMS error field, product spread or average validation error is not a simultaneous e bound. The annual and seasonal-pool restrictions are joint assumptions on the same corrupt-date set.
- Capping loses all severity information above its cap. It limits arbitrary errors partly by limiting response to real severe heat. Report it beside uncapped dose when severity matters. It is not an ecological damage forecast or a replacement for all event metrics.
- This is one product and one fixed point sample. There is no new buoy comparison, independent SST product, native-resolution replication or changing-mask analysis. The raw data overlap earlier work.
- Bounds are conservative and need not be jointly attained. Failed certificates do not prove reversals. Positive bounds are finite-record sensitivity statements, not confidence intervals, physical attribution or future projections.
- The recent endpoint and baseline choice matter. The primary guarantee does not hold through 2021 with both baselines or in the tropics with the later baseline.
- Exact source retrieval can fail if NOAA revises an annual file. The recipe refuses changed hashes. The shared dataset paths preserve the tested snapshot; aggregate evidence can be inspected without it.

The useful method is a bounded daily severity response with explicit sparse-input and threshold contamination limits. It addresses rare errors that amplitude-only certificates exclude. It does not establish that every trend affected by input changes is robust. [interpretation.md](files/interpretation.md) states the main use rules.

## Reproduction, rights and identity

[reproduce.md](files/reproduce.md) gives offline checks, complete regeneration and hash-checked retrieval into separate scratch. The package preserves original code, source identities, proof, design, aggregate evidence, figures and audits. No private scratch is required to survive. Raw SST and daily derivative arrays remain outside the signed package. All analysis processes stop before final completion.

NOAA NCEI produces OISST; NOAA PSL, Boulder, Colorado, USA provides the files. [NOTICE.md](files/NOTICE.md) gives external terms and attribution for the reused SCI extraction code. The exact SCI baseline LICENSE applies to the bundled materials and does not replace source terms. These are research outputs, not official NOAA products.

Campaign **11_07_2026**. Job **sci-1107-dell-earth-and-ocean-sciences-1cabb1c5fcf3**. Topic **earth-and-ocean-sciences**. Machine **dell**. Account **codex-myxtap**. Model **gpt-6.1-sol**, high reasoning effort. No agents were launched. The key identifies a campaign machine, not a personal author. [run.json](files/run.json) records software and run provenance. The publication is signed and verified locally, without upload or submission by this worker.
