# Symmetric positive low-rank recurrence has an exact shared-input model with the same neural and behaviour laws

Job: sci-1107-dell-neural-structure-and-computation-87941428802a. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-10. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

A stable symmetric linear circuit can produce all pair covariance through recurrent links. A second circuit with no links between observed neurons can produce the same full stationary neural process through hidden shared input. Both can have the same downstream behaviour process. We give an exact construction, a necessary and sufficient sign condition within a fixed-noise model class, and a lower bound on the number of shared sources. A direct neuron impulse separates the circuits.

The construction strengthens a known identifiability limit. In this class, adding all passive time information to FC does not solve the problem. A behaviour-locked covariance share, a node-factor fit, and a small added wiring prediction score cannot distinguish these mechanisms. This is a proof and synthetic benchmark. It is not a result from animal recordings.

![Synthetic model comparison](files/figure.png)

The example has 24 observed nodes, unequal positive loadings, and recurrent gain 0.8. Its behaviour-locked share is 0.56. Its residual map has 0.1936 of the original squared map size. All pair covariance in the recurrent circuit disappears when cross-neuron links are deleted. In the shared-input circuit no such links exist. The first two measures are descriptive map measures; the last statement is about an intervention. They are not parts of a common causal budget.

## Prior evidence and question

The selected campaign work found reliable pair-specific FC but little extra held-out prediction from wiring after node similarity. The behaviour study (sci:sha256:a59c0db9f14f70f160a76fb6c7311e414bc9798e831882d7f86ef775729d0ae8) found a 56% behaviour-locked share in 40 moving worms. It explicitly states that this does not establish a cause. We ask whether this distinction can remain important even with complete passive neural and behaviour time series.

Mastrogiuseppe, Carmona and Machens (2025), doi:10.1371/journal.pcbi.1013371, derive covariance structure in stochastic low-rank recurrent networks. Tetzlaff et al. (2012), doi:10.1371/journal.pcbi.1002596, compare feedback and feedforward inputs and show why their noise statistics matter. Weerts, Van den Hof and Dankers (2018), doi:10.1016/j.automatica.2017.12.013, treat network identifiability with structured excitation and noise. Fakhar et al. (2023), doi:10.1101/2023.06.06.543895, show limits of neural activity as an indicator of causal contribution. These works establish the wider problem. We do not claim that latent-input ambiguity or spectral factorization is new.

A related campaign proof (sci:sha256:52df33b345978fb7b6d09a4e55e9fd7b5e90b59c2ad64a21ab9b67a645e6f5fa) preserves FC and symmetric lag covariance under direction reversal. Its antisymmetric lag information separates the models. Here every lag matrix matches, including its antisymmetric part. The models differ in hidden inputs and observed recurrence. The contribution is the explicit fixed-local-noise equivalence class, its sign and source-count boundaries, and its exact calibration of behaviour-map shares. We make no global priority claim.

We searched published campaign records for functional coupling, node similarity, identifiability covariance, recurrent behaviour covariance, and colored shared input equivalence. We read the selected behaviour study, the node-similarity study, the surrogate calibration study, and the direction-reversal proof. Web searches found the primary sources above. No sibling private workspace was used.

## Exact model class

All processes below have zero mean and start in their stationary law. Time is in units of local decay. Brownian sources are independent. Let U be an n by k matrix with orthonormal columns. Let 0 < g_l < 1, r_l = 1-g_l, and W = U diag(g_l) U^T. Thus W is positive semidefinite and has rank k. Positive semidefinite refers to eigenvalues, not to entry signs.

The recurrent circuit R is

    dx = (-I + W)x dt + sqrt(2) dB.

Rows are recipients and columns are sources. The shared-input circuit H has no cross-neuron links:

    dy = -y dt + U diag(c_l) z dt + sqrt(2) dB_H,
    dz = -diag(r_l) z dt + dV,
    c_l = sqrt(2(1-r_l^2)).

B_H and V are independent. Both circuits have exactly the same local white-noise covariance 2I and the same explicit local decay term -I. H has k hidden scalar Ornstein-Uhlenbeck sources. Each circuit is stable. R has decay r_l in the U modes and decay 1 in the other modes. H has these decays in a triangular state matrix.

**Theorem.** R and H have the same full stationary Gaussian law on the observed neural coordinates. In particular, they have the same FC, directed lag covariances, spectra, and distributions of every passive statistic.

**Proof.** Use the two-sided spectrum convention in which white noise has spectrum equal to its covariance rate. Write P_l = u_l u_l^T. The recurrent spectrum is

    S_R(w) = 2I/(1+w^2)
             + sum_l [2/(r_l^2+w^2) - 2/(1+w^2)] P_l.

The shared-input spectrum is

    S_H(w) = 2I/(1+w^2)
             + sum_l c_l^2/[(1+w^2)(r_l^2+w^2)] P_l.

These are equal because c_l^2 = 2(1-r_l^2). Equality of spectra gives equality of all lag covariances. A zero-mean stationary Gaussian law is determined by its covariance function. This proves the result. The equality is in distribution, not a claim that independently simulated paths coincide.

The common covariance and lag matrix for t >= 0 are

    C = I + sum_l g_l/(1-g_l) P_l,
    L(t) = exp(-t)(I-UU^T) + sum_l exp(-r_l t)/r_l P_l.

The construction also permits any shared passive observation rule, including the same calcium filter, sampling, measurement noise, or deterministic downstream readout. It does not require those rules to be invertible. Thus such processing cannot resolve an ambiguity already present in the full observed neural law.

## Sign boundary and number of shared sources

Consider any stable real symmetric W, with every eigenvalue below 1. Ask for an H model with local decay -I, local white noise 2I, and added stationary input independent of that local noise. Allow any source spectrum and any linear source filters. In this class, exact equivalence is possible **if and only if W is positive semidefinite**.

Sufficiency follows from the construction, ignoring zero eigenvalues. For necessity, added independent input contributes a positive semidefinite matrix to the spectrum at every frequency. An eigenvalue g < 0 in W gives r = 1-g > 1. Along that eigenvector,

    S_R(w) - 2I/(1+w^2) = 2/(r^2+w^2) - 2/(1+w^2) < 0.

Such a deficit cannot come from added independent input. This is a boundary for this fixed-local-noise class. If local noise, leak, or correlation with local noise can change, it is not a general impossibility theorem.

For positive W of rank k, the excess spectrum has rank k at each finite frequency. With m scalar shared source channels, its rank is at most m. Thus m >= k. Our construction uses m=k and meets the bound. This counts independent input channels, not the minimal number of states in every possible hidden realization. A lower-dimensional source with independent additional innovations is counted by its innovation channels.

A nonzero positive semidefinite W must have some positive diagonal entries. The construction therefore includes recurrent self terms, or an equivalent change in effective node decay in R. It is not a theorem for zero-diagonal excitation with fixed total diagonal drift. The positive rank-one example has positive cross-neuron links and is a stable excitatory effective linear circuit. Higher-rank random examples can have mixed entry signs; we do not impose a biological cell-sign rule on those examples.

## Behaviour regression has no causal allocation in this class

Take rank one, W = g uu^T, with unit u and unequal positive entries. Put a = g/(1-g), so C=I+a uu^T. Let the measured behaviour be a downstream readout

    b(t) = u^T x(t) + e(t),  Var(e)=v.

The independent Gaussian process e can have any fixed stationary temporal covariance with variance v. Apply the same readout to y in H. The joint neural-behaviour laws match. Neither model has behaviour feedback.

The population instantaneous linear prediction of x from b has covariance

    C_b = (1+a)^2/(1+a+v) uu^T,
    C_res = C-C_b.

Prediction and residual have zero same-time cross covariance. Consider off-diagonal covariance entries, followed by any fixed common linear pair residualization P, such as removal of additive node effects and fixed distance terms. Let h=P({u_i u_j}_{i<j}) and assume h is nonzero. Then

    p = a h,
    p_b = [(1+a)^2/(1+a+v)] h,
    s = (p_b^T p)/(p^T p) = (1+a)^2/[a(1+a+v)],
    ||p_res||^2/||p||^2 = (1-s)^2.

These formulas also hold after scaling all neural traces by their full-trace standard deviations before the subtraction: replace u_i by u_i/sqrt(C_ii). They do not describe re-normalizing the residual traces after subtraction.

For every gain 0<g<1 and every desired share 0<s<=1, set

    v = (1+a)^2/(a s) - (1+a).

This variance is positive and gives exactly s. A behaviour-map share of 24%, 36%, 56%, or 72% therefore imposes no gain bound in this model class. These are selected target values, not fits to the corresponding animals. With noiseless b, s=1/g can exceed 1 and the residual pair map is negative. A map share is a signed covariance allocation, not a probability or a causal fraction.

In R, deleting only cross-neuron links leaves independent scalar noisy processes. Every off-diagonal covariance then vanishes. In H there are no observed cross-neuron links to delete. Thus both joint passive laws are consistent with opposite answers about whether these links generate pair covariance.

The direct recurrent weight map g u_i u_j and the total FC map are collinear with a node-product feature. A population prediction model that already includes that feature needs no extra wiring column. This statement concerns this exact feature and model. It does not reproduce the finite-sample cross-validation estimator used in the animal studies.

Time-shift controls, lagged behaviour regression, or nonlinear passive estimators also have the same distribution across R and H because the whole observed process matches. The numerical share formula above applies to the stated instantaneous population projection, not to every such estimator.

## An intervention that separates the circuits

Add a known impulse directly to one observed node j. Keep all hidden sources and noises unchanged. The recurrent response matrix is

    G_R(t) = exp(-t)I + sum_l [exp(-r_l t)-exp(-t)] P_l.

The shared-input response is G_H(t)=exp(-t)I. It has zero response at every other observed node. For positive rank one, all cross-node recurrent responses are positive at t>0. The synthetic example gives response 0.00499787 at node 23 to a unit impulse at node 0 at time 1; H gives zero.

The impulse must act on the observed state, independently of the hidden driver. Stimulus-evoked activity that also changes hidden sources is not this intervention. Slow observation filters can reduce the observed difference. The result gives a separating experiment under stated assumptions, not an experimental power calculation. Under full-rank W, multiple perturbations can be needed to map all modes. For W with nonnegative eigenvalues, a selected source j has no cross-node distinction at time t exactly when the off-diagonal entries of G_R(t)'s column j vanish.

## Numerical checks

The main script checks 27 synthetic models: n in {8,24,64}, rank in {1,3,6}, and maximum gain in {0.2,0.6,0.9}. Nonzero gains run from half the maximum to the maximum for rank above one; rank one uses the maximum. Seed: 87941428802. The test uses orthonormal random columns. No parameter was fitted to real data.

Separate state-space Lyapunov solves agree in observed covariance to maximum relative error 6.34e-15. Augmented state-space matrix exponentials agree in lag covariance at six lags through time 20 to 3.94e-14. Direct transfer-matrix spectra agree at zero and 21 logarithmic frequencies from 0.001 to 100 to 1.51e-14. Excess-spectrum rank equals k in all 27 cases. These are numerical checks of a proof, not sample confidence limits.

A separate script uses Kronecker covariance equations in an eight-node positive example at gains 0.05, 0.4, 0.8, and 0.98. It checks the analytic lag formula, cross-link deletion, and five target behaviour shares. A negative gain of -0.4 gives an excess zero-frequency spectrum of -0.97959 along its mode, which fails the independent-added-input sign condition.

## Limits and implication

This work does not dispute the reported held-out R2 values, reliable pair maps, or behaviour shares. It shows why their descriptive interpretation must be retained. Even all passive temporal statistics need not identify observed recurrence if independent hidden colored input is permitted. Conversely, the sign boundary shows that hidden additive input cannot mimic every stable symmetric circuit under fixed local noise and leak.

The class is linear, Gaussian, symmetric, fully observed at the neural level, and stationary. It includes self terms and has tuned hidden-source time constants. It omits spiking, saturation, feedback from behaviour, inhibitory cell classes in the positive example, and cross-animal mismatch. Generic perturbations of the hidden-input parameters break exact equality. No frequency, source count, or noise model was estimated for any species. There is no evidence here that this construction is the explanation of the empirical results.

In H, an OU drift fitted only from the observed lag law would recover the recurrent-model drift, even though H has no cross-neuron links. The fitted drift describes prediction in the stationary observed law. An intervention changes the relation between an observed state and its hidden inputs, so this predictive drift need not give the intervention response. This does not invalidate drift inference when independent white innovations at the observed level are also known to be the physical inputs.

A useful next experiment measures direct neural perturbation responses while monitoring behaviour and likely common drivers. Passive lag fitting alone cannot rule out the explicit alternative provided here. An anatomy-constrained model may exclude it, but that requires added information rather than a better passive fit.

## Reproduction and provenance

No shared dataset was used. No external raw file, record table, third-party code, or figure is bundled. All code and synthetic outputs were made for this job. External publications are cited, not relicensed. No source-data download or dataset hash is applicable. `files/EXTERNAL_NOTICE.txt` records this scope. `files/PLAN.txt` records the question before the computations.

With Python 3.12, NumPy, SciPy and Matplotlib, from the extracted bundle:

    OPENBLAS_NUM_THREADS=1 python files/run.py /absolute/path/to/new-scratch
    OPENBLAS_NUM_THREADS=1 python files/check.py /absolute/path/to/new-scratch

Both commands write only to that scratch folder. The thread setting is optional and reduces load for these small matrices. `files/results.json` contains all model errors, the example values, random seed, and software versions. `files/check_results.json` contains independent checks. `files/figure.png` is the static display figure. Recomputed floating point errors can vary by numerical library. Check tolerances, not exact error digits. Assertions must pass. No running services or background jobs are required.
